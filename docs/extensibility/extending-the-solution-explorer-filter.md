---
title: ソリューションエクスプローラー Filter | の拡張Microsoft Docs
description: ソリューションエクスプローラーフィルター機能を拡張して、Visual Studio SDK のさまざまなファイルを表示または非表示にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Solution Explorer, extending
- extensibility [Visual Studio], projects and solutions
ms.assetid: df976c76-27ec-4f00-ab6d-a26a745dc6c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cde3377582c3bac0c27371e25f28e5151d641db1
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994564"
---
# <a name="extend-the-solution-explorer-filter"></a>ソリューションエクスプローラーフィルターを拡張する
**ソリューションエクスプローラー** フィルター機能を拡張して、さまざまなファイルの表示と非表示を切り替えることができます。 たとえば、このチュートリアルで示すように、 **ソリューションエクスプローラー** に C# クラスファクトリファイルのみを表示するフィルターを作成できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-visual-studio-package-project"></a>Visual Studio パッケージプロジェクトを作成する

1. という名前の VSIX プロジェクトを作成 `FileFilter` します。 **FileFilter** という名前のカスタムコマンド項目テンプレートを追加します。 詳細については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

2. およびへの参照を追加し `System.ComponentModel.Composition` `Microsoft.VisualStudio.Utilities` ます。

3. メニューコマンドが **ソリューションエクスプローラー** ツールバーに表示されるようにします。 *Filefilterpackage. vsct* ファイルを開きます。

4. ブロックを `<Button>` 次のように変更します。

    ```xml
    <Button guid="guidFileFilterPackageCmdSet" id="FileFilterId" priority="0x0400" type="Button">
        <Parent guid="guidSHLMainMenu" id="IDG_VS_TOOLBAR_PROJWIN_FILTERS" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>FileNameFilter</ButtonText>
        </Strings>
    </Button>
    ```

### <a name="update-the-manifest-file"></a>マニフェスト ファイルを更新する

1. *Source.extension.vsixmanifest* ファイルで、MEF コンポーネントであるアセットを追加します。

2. [ **アセット** ] タブで、[ **新規** ] ボタンをクリックします。

3. [ **種類** ] フィールドで、[ **VisualStudio**] を選択します。

4. [ **ソース** ] フィールドで、 **現在のソリューション内のプロジェクト** を選択します。

5. [ **プロジェクト** ] フィールドで [ **FileFilter**] を選択し、[ **OK** ] をクリックします。

### <a name="add-the-filter-code"></a>フィルターコードを追加する

1. いくつかの Guid を *FileFilterPackageGuids.cs* ファイルに追加します。

    ```csharp
    public const string guidFileFilterPackageCmdSetString = "00000000-0000-0000-0000-00000000"; // get your GUID from the .vsct file
    public const int FileFilterId = 0x100;
    ```

2. *FileNameFilter.cs* という名前の FileFilter プロジェクトにクラスファイルを追加します。

3. 空の名前空間と空のクラスを次のコードに置き換えます。

     メソッドは、 `Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem rootItems)` ソリューションのルート () を含むコレクションを取得 `rootItems` し、フィルターに含める項目のコレクションを返します。

     メソッドは、指定した `ShouldIncludeInFilter` 条件に基づいて、 **ソリューションエクスプローラー** 階層内の項目をフィルター処理します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio.Shell;

    namespace FileFilter
    {
        // Implements ISolutionTreeFilterProvider. The SolutionTreeFilterProvider attribute declares it as a MEF component
        [SolutionTreeFilterProvider(FileFilterPackageGuids.guidFileFilterPackageCmdSetString, (uint)(FileFilterPackageGuids.FileFilterId))]
        public sealed class FileNameFilterProvider : HierarchyTreeFilterProvider
        {
            SVsServiceProvider svcProvider;
            IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;

            // Constructor required for MEF composition
            [ImportingConstructor]
            public FileNameFilterProvider(SVsServiceProvider serviceProvider, IVsHierarchyItemCollectionProvider hierarchyCollectionProvider)
            {
                this.svcProvider = serviceProvider;
                this.hierarchyCollectionProvider = hierarchyCollectionProvider;
            }

            // Returns an instance of Create filter class.
            protected override HierarchyTreeFilter CreateFilter()
            {
                return new FileNameFilter(this.svcProvider, this.hierarchyCollectionProvider, FileNamePattern);
            }

            // Regex pattern for CSharp factory classes
            private const string FileNamePattern = @"\w*factory\w*(.cs$)";

            // Implementation of file filtering
            private sealed class FileNameFilter : HierarchyTreeFilter
            {
                private readonly Regex regexp;
                private readonly IServiceProvider svcProvider;
                private readonly IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;

                public FileNameFilter(
                    IServiceProvider serviceProvider,
                    IVsHierarchyItemCollectionProvider hierarchyCollectionProvider,
                    string fileNamePattern)
                {
                    this.svcProvider = serviceProvider;
                    this.hierarchyCollectionProvider = hierarchyCollectionProvider;
                    this.regexp = new Regex(fileNamePattern, RegexOptions.IgnoreCase);
                }

                // Gets the items to be included from this filter provider.
                // rootItems is a collection that contains the root of your solution
                // Returns a collection of items to be included as part of the filter
                protected override async Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem> rootItems)
                {
                    IVsHierarchyItem root = HierarchyUtilities.FindCommonAncestor(rootItems);
                    IReadOnlyObservableSet<IVsHierarchyItem> sourceItems;
                    sourceItems = await hierarchyCollectionProvider.GetDescendantsAsync(
                                        root.HierarchyIdentity.NestedHierarchy,
                                        CancellationToken);

                    IFilteredHierarchyItemSet includedItems = await hierarchyCollectionProvider.GetFilteredHierarchyItemsAsync(
                        sourceItems,
                        ShouldIncludeInFilter,
                        CancellationToken);
                    return includedItems;
                }

                // Returns true if filters hierarchy item name for given filter; otherwise, false</returns>
                private bool ShouldIncludeInFilter(IVsHierarchyItem hierarchyItem)
                {
                    if (hierarchyItem == null)
                    {
                        return false;
                    }
                    return this.regexp.IsMatch(hierarchyItem.Text);
                }
            }
        }
    }

    ```

4. *FileFilter.cs* で、FileFilter コンストラクターからコマンド配置および処理コードを削除します。 結果は次のようになります。

    ```csharp
    private FileFilter(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;
    }
    ```

     `ShowMessageBox()`メソッドも削除します。

5. *FileFilterPackage.cs* で、メソッド内のコードを `Initialize()` 次のコードに置き換えます。

    ```csharp
    protected override void Initialize()
    {
        Debug.WriteLine (string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));
        base.Initialize();
    }
    ```

### <a name="test-your-code"></a>コードのテスト

1. プロジェクトをビルドして実行します。 Visual Studio の 2 番目のインスタンスが表示されます。 これは実験用インスタンスと呼ばれます。

2. Visual Studio の実験用インスタンスで、C# プロジェクトを開きます。

3. **ソリューションエクスプローラー** ツールバーで追加したボタンを探します。 左側の4番目のボタンになります。

4. このボタンをクリックすると、すべてのファイルが除外さ **れ、すべての項目がビューからフィルター処理され** ていることがわかります。 **ソリューションエクスプローラー** にあります。
