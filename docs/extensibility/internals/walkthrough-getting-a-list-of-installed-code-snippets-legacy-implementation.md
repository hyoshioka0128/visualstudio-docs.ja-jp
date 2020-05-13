---
title: インストール済みコード スニペットの一覧の取得 (レガシ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, retrieving list
- code snippets, retrieving list
- GetSnippets method
ms.assetid: 7d142f8b-35b1-44c4-a13e-f89f6460c906
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d3d5ef857973555c4b2d201f98957bd2c39328b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703651"
---
# <a name="walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation"></a>チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)
コード スニペットは、メニュー コマンド (インストール済みコード スニペットの一覧から選択できる) を使用するか、IntelliSense コンプリート リストからスニペット ショートカットを選択することで、ソース バッファーに挿入できるコードの一部です。

 この<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.EnumerateExpansions%2A>メソッドは、特定の言語 GUID のすべてのコード スニペットを取得します。 これらのスニペットのショートカットは、IntelliSense コンプリート リストに挿入できます。

 マネージ パッケージ フレームワーク (MPF)[言語サービスでのコード スニペット](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)の実装の詳細については、「レガシ言語サービスでのコード スニペットのサポート」をご覧ください。

### <a name="to-retrieve-a-list-of-code-snippets"></a>コード スニペットの一覧を取得するには

1. 次のコードは、特定の言語のコード スニペットの一覧を取得する方法を示しています。 結果は<xref:Microsoft.VisualStudio.TextManager.Interop.VsExpansion>構造体の配列に格納されます。 このメソッドは、静的<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>メソッドを使用して<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager>、サービスから<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>インターフェイスを取得します。 ただし、VSPackage に与えられたサービス プロバイダーを使用してメソッドを<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>呼び出すこともできます。

    ```csharp
    using System;
    using System.Collections;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Package;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.TextManager.Interop;

    [Guid("00000000-0000-0000-0000-000000000000")] //create a new GUID for the language service
    namespace TestLanguage
    {
        class TestLanguageService : LanguageService
        {
            private void GetSnippets(Guid languageGuid,
                                     ref ArrayList expansionsList)
            {
                IVsTextManager textManager = (IVsTextManager)Package.GetGlobalService(typeof(SVsTextManager));
                if (textManager != null)
                {
                    IVsTextManager2 textManager2 = (IVsTextManager2)textManager;
                    if (textManager2 != null)
                    {
                        IVsExpansionManager expansionManager = null;
                        textManager2.GetExpansionManager(out expansionManager);
                        if (expansionManager != null)
                        {
                            // Tell the environment to fetch all of our snippets.
                            IVsExpansionEnumeration expansionEnumerator = null;
                            expansionManager.EnumerateExpansions(languageGuid,
                            0,     // return all info
                            null,    // return all types
                            0,     // return all types
                            1,     // include snippets without types
                            0,     // do not include duplicates
                            out expansionEnumerator);
                            if (expansionEnumerator != null)
                            {
                                // Cache our expansions in a VsExpansion array
                                uint count   = 0;
                                uint fetched = 0;
                                VsExpansion expansionInfo = new VsExpansion();
                                IntPtr[] pExpansionInfo   = new IntPtr[1];

                                // Allocate enough memory for one VSExpansion structure. This memory is filled in by the Next method.
                                pExpansionInfo[0] = Marshal.AllocCoTaskMem(Marshal.SizeOf(expansionInfo));

                                expansionEnumerator.GetCount(out count);
                                for (uint i = 0; i < count; i++)
                                {
                                    expansionEnumerator.Next(1, pExpansionInfo, out fetched);
                                    if (fetched > 0)
                                    {
                                        // Convert the returned blob of data into a structure that can be read in managed code.
                                        expansionInfo = (VsExpansion)Marshal.PtrToStructure(pExpansionInfo[0], typeof(VsExpansion));

                                        if (!String.IsNullOrEmpty(expansionInfo.shortcut))
                                        {
                                            expansionsList.Add(expansionInfo);
                                        }
                                    }
                                }
                                Marshal.FreeCoTaskMem(pExpansionInfo[0]);
                            }
                        }
                    }
                }
            }
        }
    }
    ```

### <a name="to-call-the-getsnippets-method"></a>メソッドを呼び出すには

1. 次のメソッドは、解析操作の`GetSnippets`完了時にメソッドを呼び出す方法を示しています。 メソッド<xref:Microsoft.VisualStudio.Package.LanguageService.OnParseComplete%2A>は、 理由<xref:Microsoft.VisualStudio.Package.ParseReason>で開始された解析操作の後に呼び出されます。

> [!NOTE]
> `expansionsList`アレイ・リストは、パフォーマンス上の理由からキャッシュされます。 スニペットに対する変更は、言語サービスが停止して再読み込みされるまでリストに反映されません (たとえば、停止して再起動[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]するなど)。

```csharp
class TestLanguageService : LanguageService
{
    private ArrayList expansionsList;

    public override void OnParseComplete(ParseRequest req)
    {
        if (this.expansionsList == null)
        {
            this.expansionsList = new ArrayList();
            GetSnippets(this.GetLanguageServiceGuid(),
                ref this.expansionsList);
        }
    }
}
```

### <a name="to-use-the-snippet-information"></a>スニペット情報を使用するには

1. 次のコードは、メソッドによって返されるスニペット情報の使用方法`GetSnippets`を示しています。 この`AddSnippets`メソッドは、コード スニペットの一覧を設定するために使用される解析の理由に応じてパーサーから呼び出されます。 これは、完全解析が初めて行われた後に行われます。

     この`AddDeclaration`メソッドは、後で完了リストに表示される宣言のリストを作成します。

     この`TestDeclaration`クラスには、完了リストに表示できるすべての情報と宣言の種類が含まれます。

    ```csharp
    class TestAuthoringScope : AuthoringScope
    {
        public void AddDeclarations(TestDeclaration declaration)
        {
            if (m_declarations == null)
                m_declarations = new List<TestDeclaration>();
            m_declarations.Add(declaration);
         }
    }
    class TestDeclaration
    {
        private string m_name;
        private string m_description;
        private string m_type;

        public TestDeclaration(string name, string desc, string type)
        {
            m_name = name;
            m_description = desc;
            m_type = type;
        }

    class TestLanguageService : LanguageService
    {
        internal void AddSnippets(ref TestAuthoringScope scope)
        {
            if (this.expansionsList != null && this.expansionsList.Count > 0)
            {
                int count = this.expansionsList.Count;
                for (int i = 0; i < count; i++)
                {
                    VsExpansion expansionInfo = (VsExpansion)this.expansionsList[i];
                    scope.AddDeclaration(new TestDeclaration(expansionInfo.title,
                         expansionInfo.description,
                         "snippet"));
                }
            }
        }
    }

    ```

## <a name="see-also"></a>関連項目
- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)
