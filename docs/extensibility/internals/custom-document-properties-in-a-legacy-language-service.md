---
title: 従来の言語サービスのカスタム ドキュメント プロパティ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom document properties, language services [managed package framework]
- document properties, custom
- language services [managed package framework], custom document properties
ms.assetid: cc714a67-b33e-4440-9203-3c90f648bd9c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1b3db7f4cfa45ea96e3da3056f39c2a5c78a25ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708966"
---
# <a name="custom-document-properties-in-a-legacy-language-service"></a>従来の言語サービスのカスタム ドキュメント プロパティ
ドキュメントプロパティは、[[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**プロパティ]** ウィンドウに表示できます。 プログラミング言語には、通常、個々のソース ファイルに関連付けられたプロパティはありません。 ただし、XML では、エンコード、スキーマ、およびスタイルシートに影響を与えるドキュメント プロパティがサポートされます。

## <a name="discussion"></a>ディスカッション
 言語にカスタム ドキュメント プロパティが必要な場合は、クラスから<xref:Microsoft.VisualStudio.Package.DocumentProperties>クラスを派生させ、派生クラスに必要なプロパティを実装する必要があります。

 また、ドキュメント プロパティは通常、ソース ファイル自体に格納されます。 そのためには、言語サービスがソース ファイルのプロパティ情報を解析して **[プロパティ]** ウィンドウに表示し、[**プロパティ]** ウィンドウでドキュメント プロパティが変更されたときにソース ファイルを更新する必要があります。

## <a name="customize-the-documentproperties-class"></a>クラスをカスタマイズする
 カスタム ドキュメント プロパティをサポートするには、<xref:Microsoft.VisualStudio.Package.DocumentProperties>クラスからクラスを派生させ、必要な数のプロパティを追加する必要があります。 また、ユーザー属性を指定して **、[プロパティ]** ウィンドウの表示で構成する必要があります。 プロパティにアクセサーのみが含`get`まれる場合は、[**プロパティ]** ウィンドウに読み取り専用として表示されます。 プロパティにアクセサーと`get``set`アクセサーの両方がある場合は、プロパティウィンドウでも**プロパティ**を更新できます。

### <a name="example"></a>例
 2 つのプロパティと<xref:Microsoft.VisualStudio.Package.DocumentProperties>から派生したクラスの例`Filename`を`Description`次に示します。 プロパティが更新されると、<xref:Microsoft.VisualStudio.Package.LanguageService>クラスのカスタム メソッドが呼び出され、プロパティがソース ファイルに書き込まれます。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestDocumentProperties : DocumentProperties
    {
        private string m_filename;
        private string m_description;

        public TestDocumentProperties(CodeWindowManager mgr)
            : base(mgr)
        {
        }

        // Helper function to initialize this property without
        // going through the FileName property (which does a lot
        // more than we need when the filename is set).
        public void SetFileName(string filename)
        {
            m_filename = filename;
        }

        // Helper function to initialize this property without
        // going through the Description property (which does a lot
        // more than we need when the description is set).
        public void SetDescription(string description)
        {
            m_description = description;
        }

        ////////////////////////////////////////////////////////////
        // The document properties

        [CategoryAttribute("General")]
        [DescriptionAttribute("Name of the file")]
        [DisplayNameAttribute("Filename")]
        public string FileName
        {
            get { return m_filename; }
            set
            {
               if (value != m_filename)
               {
                    m_filename = value;
                    SetPropertyValue("Filename", m_filename);
               }
            }
        }

        [CategoryAttribute("General")]
        [DescriptionAttribute("Description of the file")]
        [DisplayNameAttribute("Description")]
        public string Description
        {
            get { return m_description; }
            set
            {
                if (value != m_description)
                {
                    m_description = value;
                    SetPropertyValue("Description", m_description);
                }
            }
        }

        ///////////////////////////////////////////////////////////
        // Private methods.

        private void SetPropertyValue(string propertyName, string propertyValue)
        {
            Source src = this.GetSource();
            if (src != null)
            {
                TestLanguageService service = src.LanguageService as TestLanguageService;
                if (service != null)
                {
                    // Set the property in to the source file.
                    service.SetPropertyValue(src, propertyName, propertyValue);
                }
            }
        }
    }
}
```

## <a name="instantiate-the-custom-documentproperties-class"></a>カスタム ドキュメント プロパティ クラスのインスタンスを作成します。
 カスタム ドキュメント プロパティ クラスをインスタンス化するには、<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A><xref:Microsoft.VisualStudio.Package.LanguageService>クラスのバージョンのメソッドをオーバーライドして、クラスの 1<xref:Microsoft.VisualStudio.Package.DocumentProperties>つのインスタンスを返す必要があります。

### <a name="example"></a>例

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        private TestDocumentProperties m_documentProperties;

        public override DocumentProperties CreateDocumentProperties(CodeWindowManager mgr)
        {
            if (m_documentProperties == null)
            {
                m_documentProperties = new TestDocumentProperties(mgr);
            }
            return m_documentProperties;
        }
    }
}
```

## <a name="properties-in-the-source-file"></a>ソース ファイルのプロパティ
 ドキュメント プロパティは通常、ソース ファイルに固有であるため、値はソース ファイル自体に格納されます。 これらのプロパティを定義するには、言語パーサーまたはスキャナーのサポートが必要です。 たとえば、XML ドキュメントのプロパティはルート ノードに格納されます。 ルート ノードの値は **、[プロパティ]** ウィンドウの値が変更されると変更され、ルート ノードがエディターで更新されます。

### <a name="example"></a>例
 この例では`Filename`、次のように`Description`プロパティを格納し、ソース ファイルの最初の 2 行に特別なコメント ヘッダーに埋め込みます。

```
//!Filename = file.testext
//!Description = A sample file
```

 この例では、ソース ファイルの最初の 2 行からドキュメント プロパティを取得および設定するために必要な 2 つのメソッドと、ユーザーがソース ファイルを直接変更した場合にプロパティを更新する方法を示します。 ここで`SetPropertyValue`示す例のメソッドは`TestDocumentProperties`*、DocumentProperties*クラスのカスタマイズセクションに示されているクラスから呼び出されるメソッドと同じです。

 この例では、スキャナーを使用して、最初の 2 行のトークンの種類を確認します。 この例は、説明のみを目的とします。 この状況に対する一般的なアプローチは、ソース ファイルを解析して、ツリーの各ノードに特定のトークンに関する情報が含まれる解析ツリーと呼ばれるものにします。 ルート ノードには、ドキュメント プロパティが含まれます。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    // TokenType.Comment is the last item in that enumeration.
    public enum TestTokenTypes
    {
        DocPropertyLine = TokenType.Comment + 1,
        DocPropertyName,
        DocPropertyAssign,
        DocPropertyValue
    }

    class TestLanguageService : LanguageService
    {
        // Search this many lines from the beginning for properties.
        private static int maxLinesToSearch = 2;

        private TestDocumentProperties m_documentProperties;

        // Called whenever a full parsing operation has completed.
        public override void OnParseComplete(ParseRequest req)
        {
            if (m_documentProperties != null)
            {
                Source src = GetSource(req.View);
                if (src != null)
                {
                    string value = GetPropertyValue(src, "Filename");
                    m_documentProperties.SetFileName(value);

                    value = GetPropertyValue(src, "Description");
                    m_documentProperties.SetDescription(value);

                    // Update the Properties Window.
                    m_documentProperties.Refresh();
                }
            }
        }

        // Retrieves the specified property value from the given source.
        public string GetPropertyValue(Source src, string propertyName)
        {
            string propertyValue = "";

            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    string      line;
                    TokenInfo[] lineInfo = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line.
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                for ( ;
                                     tokenIndex < lineInfo.Length;
                                     tokenIndex++)
                                {
                                    if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyValue)
                                    {
                                        break;
                                    }
                                }
                                if (tokenIndex < lineInfo.Length)
                                {
                                    propertyValue = src.GetText(i,
                                                          lineInfo[tokenIndex].StartIndex,
                                                          i,
                                                          lineInfo[tokenIndex].EndIndex + 1);
                                }
                                break;
                            }
                        }
                    }
                }
            }
            return propertyValue;
        }

        // Sets the specified property into the given source file.
        // Called from the TestDocumentProperties class.
        public void SetPropertyValue(Source src, string propertyName, string propertyValue)
        {
            string newLine;

            if (propertyName == null || propertyName == "")
            {
                // No property name, so nothing to do
                return;
            }
            if (propertyValue == null)
            {
                propertyValue = "";
            }
            // This is the line to be inserted.
            newLine = String.Format("//!{0} = {1}", propertyName, propertyValue);

            // First, find the line on which the property belongs.
            // If line is found, replace it.
            // Otherwise, insert the line at the beginning of the file.
            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    int         lineNumber = -1;
                    string      line;
                    TokenInfo[] lineInfo   = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                lineNumber = i;
                                break;
                            }
                        }
                    }

                    // Set up an undo context that also handles the insert/replace.
                    EditArray editArray = new EditArray(src,
                                                        true,
                                                        "Update Property");
                    if (editArray != null)
                    {
                        TextSpan span = new TextSpan();
                        if (lineNumber != -1)
                        {
                            // Replace line.
                            int lineLength = 0;
                            src.GetTextLines().GetLengthOfLine(lineNumber,
                                                               out lineLength);
                            span.iStartLine  = lineNumber;
                            span.iStartIndex = 0;
                            span.iEndLine    = lineNumber;
                            span.iEndIndex   = lineLength;
                        }
                        else
                        {
                            // Insert new line.
                            span.iStartLine  = 0;
                            span.iStartIndex = 0;
                            span.iEndLine    = 0;
                            span.iEndIndex   = 0;
                            newLine += "\n";
                        }
                        editArray.Add(new EditSpan(span, newLine));
                        editArray.ApplyEdits();
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービス機能](../../extensibility/internals/legacy-language-service-features1.md)
