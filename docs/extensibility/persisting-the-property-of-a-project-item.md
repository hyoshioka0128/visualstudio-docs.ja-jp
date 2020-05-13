---
title: プロジェクト項目のプロパティを永続化する |マイクロソフトドキュメント
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15c280f15436a5e27bcc0dcc4d2fb9e9bdd82933
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702202"
---
# <a name="persist-the-property-of-a-project-item"></a>プロジェクト項目のプロパティを永続化する
ソース ファイルの作成者など、プロジェクト項目に追加するプロパティを永続化できます。 これを行うには、プロジェクト ファイルにプロパティを格納します。

 プロジェクト ファイルにプロパティを永続化する最初の手順は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>プロジェクトの階層をインターフェイスとして取得することです。 このインターフェイスは、オートメーションを使用するか、または を<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>使用して取得できます。 インターフェイスを取得したら、そのインターフェイスを使用して、現在選択されているプロジェクト項目を確認できます。 プロジェクト項目 ID を取得したら、 を<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A>使用してプロパティを追加できます。

 次の手順では *、VsPkg.cs*プロパティ`Author`をプロジェクト ファイルの値`Tom`で永続化します。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>DTE オブジェクトを使用してプロジェクト階層を取得するには

1. VS パッケージに次のコードを追加します。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>DTE オブジェクトを使用してプロジェクト項目のプロパティを永続化するには

1. 前の手順のメソッドで指定したコードに次のコードを追加します。

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item(
            "VsPkg.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>IVsMonitorSelection を使用してプロジェクト階層を取得するには

1. VS パッケージに次のコードを追加します。

    ```csharp
    IVsHierarchy hierarchy = null;
    IntPtr hierarchyPtr = IntPtr.Zero;
    IntPtr selectionContainer = IntPtr.Zero;
    uint itemid;

    // Retrieve shell interface in order to get current selection
    IVsMonitorSelection monitorSelection =     Package.GetGlobalService(typeof(SVsShellMonitorSelection)) as     IVsMonitorSelection;
    if (monitorSelection == null)
        throw new InvalidOperationException();

    try
    {
        // Get the current project hierarchy, project item, and selection container for the current selection
        // If the selection spans multiple hierachies, hierarchyPtr is Zero
        IVsMultiItemSelect multiItemSelect = null;
        ErrorHandler.ThrowOnFailure(
            monitorSelection.GetCurrentSelection(
                out hierarchyPtr, out itemid,
                out multiItemSelect, out selectionContainer));

        // We only care if there is only one node selected in the tree
        if (!(itemid == VSConstants.VSITEMID_NIL ||
            hierarchyPtr == IntPtr.Zero ||
            multiItemSelect != null ||
            itemid == VSConstants.VSITEMID_SELECTION))
        {
            hierarchy = Marshal.GetObjectForIUnknown(hierarchyPtr)
                as IVsHierarchy;
        }
    }
    finally
    {
        if (hierarchyPtr != IntPtr.Zero)
            Marshal.Release(hierarchyPtr);
        if (selectionContainer != IntPtr.Zero)
            Marshal.Release(selectionContainer);
    }
    ```

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>プロジェクト階層を指定して、選択したプロジェクト項目のプロパティを永続化するには

1. 前の手順のメソッドで指定したコードに次のコードを追加します。

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>プロパティが永続化されていることを確認するには

1. ソリューション[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を開始して開くか、または作成します。

2. **ソリューション エクスプローラー**でVsPkg.csプロジェクト項目を選択します。

3. ブレークポイントを使用するか、VSPackage が読み込まれ、SetItemAttribute が実行されることを判断します。

   > [!NOTE]
   > VSPackage を UI コンテキスト<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>で自動ロードできます。 詳細については、「 [VS パッケージの読み込み](../extensibility/loading-vspackages.md)」を参照してください。

4. プロジェクト[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ファイルを閉じて、メモ帳で開きます。 次のように、値\<Tom を持つ著者>タグが表示されます。

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>関連項目

- [カスタム ツール](../extensibility/internals/custom-tools.md)
