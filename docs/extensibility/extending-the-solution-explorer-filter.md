---
title: ソリューション エクスプローラー フィルターの拡張 |マイクロソフトドキュメント
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
ms.openlocfilehash: af0824edd4188481bec8c0703d71043354f5dbcc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711569"
---
# <a name="extend-the-solution-explorer-filter"></a>ソリューション エクスプローラー フィルターを拡張する
**ソリューション エクスプローラー**のフィルター機能を拡張して、さまざまなファイルを表示または非表示にすることができます。 たとえば、このチュートリアルで示すように、**ソリューション エクスプローラー**で C# クラス ファクトリ ファイルのみを表示するフィルターを作成できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-visual-studio-package-project"></a>Visual Studio パッケージ プロジェクトを作成する

1. という名前`FileFilter`の VSIX プロジェクトを作成します。 **FileFilter**という名前のカスタム コマンド項目テンプレートを追加します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. への参照を`System.ComponentModel.Composition`追加します`Microsoft.VisualStudio.Utilities`。

3. **ソリューション エクスプローラー**のツール バーにメニュー コマンドを表示します。 *ファイルを*開きます。

4. ブロックを`<Button>`次のように変更します。

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

1. *source.extension.vsixmanifest*ファイルに、MEF コンポーネントである資産を追加します。

2. [**アセット**] タブで、[**新規**] ボタンを選択します。

3. [**タイプ]** フィールド**で、[コンポーネント]** を選択します。

4. [**ソース**] フィールド**で、[現在のソリューションのプロジェクト**] を選択します。

5. [**プロジェクト**] フィールド**で、[ファイル フィルタ**] をクリックし **、[OK] をクリックします**。

### <a name="add-the-filter-code"></a>フィルタ コードを追加する

1. *FileFilterPackageGuids.cs*ファイルにいくつかの GUID を追加します。

    ```csharp
    public const string guidFileFilterPackageCmdSetString = "00000000-0000-0000-0000-00000000"; // get your GUID from the .vsct file
    public const int FileFilterId = 0x100;
    ```

2. FileNameFilter.cs という名前の FileFilter プロジェクトにクラス ファイル*を*追加します。

3. 空の名前空間と空のクラスを次のコードに置き換えます。

     この`Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem rootItems)`メソッドは、ソリューションのルート (`rootItems`) を含むコレクションを受け取り、フィルターに含める項目のコレクションを返します。

     この`ShouldIncludeInFilter`メソッドは、指定した条件に基づいて **、ソリューション エクスプローラー**階層内の項目をフィルター処理します。

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

4. *FileFilter.cs*で、FileFilter コンストラクタからコマンドの配置と処理コードを削除します。 結果は次のようになります。

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

     メソッドも`ShowMessageBox()`削除します。

5. FileFilterPackage.cs*で*、メソッドのコードを`Initialize()`次のように置き換えます。

    ```csharp
    protected override void Initialize()
    {
        Debug.WriteLine (string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));
        base.Initialize();
    }
    ```

### <a name="test-your-code"></a>コードのテスト

1. プロジェクトをビルドして実行します。 Visual Studio の 2 番目のインスタンスが表示されます。 これを実験インスタンスと呼ばれます。

2. Visual Studio の実験用インスタンスで、C# プロジェクトを開きます。

3. **ソリューション エクスプローラー**のツール バーに追加したボタンを探します。 左から 4 番目のボタンにする必要があります。

4. ボタンをクリックすると、すべてのファイルが除外され、**すべてのアイテムがビューからフィルタ処理されていることがわかります。** ソリューション**エクスプローラ**で、
