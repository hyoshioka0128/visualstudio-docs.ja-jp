---
title: プロジェクト項目のプロパティを永続化 |Microsoft Docs
ms.date: 03/22/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: da231c924e3167a50c885cf18ef878a02b28b166
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915582"
---
# <a name="persist-the-property-of-a-project-item"></a>プロジェクト項目のプロパティを永続化します。
ソース ファイルの作成者などのプロジェクト項目に追加するプロパティを保持することがあります。 プロジェクト ファイルでプロパティを格納することで、これを行うことができます。

 プロジェクト ファイルのプロパティを永続化する最初の手順は、プロジェクトの階層を取得する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>インターフェイス。 このインターフェイスを取得するには、オートメーションを使用して、またはを使用して<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>します。 インターフェイスを取得した後は、どのプロジェクト項目が現在選択されているかを判断するのに使用できます。 使用することができます、プロジェクト項目の ID を作成したら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A>プロパティを追加します。

 永続化する次の手順で、 *VsPkg.cs*プロパティ`Author`値を持つ`Tom`プロジェクト ファイル。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>DTE オブジェクトをプロジェクトの階層を取得するには

1.  次のコードを VSPackage に追加します。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>DTE オブジェクトとプロジェクト項目のプロパティを永続化するには

1.  メソッドで、前の手順で指定されたコードには、次のコードを追加します。

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

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>IVsMonitorSelection を使用して、プロジェクト階層を取得するには

1.  次のコードを VSPackage に追加します。

    ```csharp
    IVsHierarchy hierarchy = null;
    IntPtr hierarchyPtr = IntPtr.Zero;
    IntPtr selectionContainer = IntPtr.Zero;
    uint itemid;

    // Retrieve shell interface in order to get current selection
    IVsMonitorSelection monitorSelection =     Package.GetGlobalService(typeof(SVsShellMonitorSelection)) as     IVsMonitorSelection;
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

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>プロジェクトの階層を指定された、選択したプロジェクト項目のプロパティを永続化するには

1.  メソッドで、前の手順で指定されたコードには、次のコードを追加します。

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>プロパティが保持されていることを確認するには

1. 開始[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]開くか、ソリューションを作成します。

2. プロジェクトを選択項目で VsPkg.cs**ソリューション エクスプ ローラー**します。

3. ブレークポイントを使用して、またはそれ以外の場合、VSPackage が読み込まれていると、SetItemAttribute が実行されることを確認します。

   > [!NOTE]
   > UI のコンテキストで VSPackage を自動読み込みを実行できます<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>します。 詳細については、次を参照してください。[ロード Vspackage](../extensibility/loading-vspackages.md)します。

4. 閉じる[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]し、メモ帳でプロジェクト ファイルを開きます。 表示する必要があります、\<作成者 > 次のように、値は、Tom タグします。

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>関連項目

- [カスタム ツール](../extensibility/internals/custom-tools.md)