---
title: プロジェクト項目のプロパティを永続化する |Microsoft Docs
description: プロジェクト項目に追加するプロパティを永続化する方法については、拡張されたプロジェクトの種類のプロジェクトファイルにプロパティを格納する方法に関するページを参照してください。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58c46da9023cc64246f1ea9ee4bde1ec866c545d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090357"
---
# <a name="persist-the-property-of-a-project-item"></a>プロジェクト項目のプロパティを保持する
ソースファイルの作成者など、プロジェクト項目に追加したプロパティを永続化することもできます。 これを行うには、プロパティをプロジェクトファイルに格納します。

 プロジェクトファイルでプロパティを永続化するための最初の手順は、プロジェクトの階層をインターフェイスとして取得することです <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 このインターフェイスは、オートメーションを使用するか、を使用して取得でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> ます。 インターフェイスを取得したら、それを使用して、現在選択されているプロジェクト項目を特定できます。 プロジェクト項目 ID を取得したら、を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> プロパティを追加できます。

 次の手順では、 *VsPkg* プロパティを `Author` プロジェクトファイルの値と共に保持します `Tom` 。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>DTE オブジェクトを使用してプロジェクト階層を取得するには

1. VSPackage に次のコードを追加します。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>DTE オブジェクトを使用してプロジェクト項目のプロパティを保持するには

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

1. VSPackage に次のコードを追加します。

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

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>プロジェクト階層の指定により、選択したプロジェクト項目のプロパティを永続化するには

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

1. を起動 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] し、ソリューションを開くか、作成します。

2. **ソリューションエクスプローラー** でプロジェクト項目 VsPkg を選択します。

3. ブレークポイントを使用するか、または VSPackage が読み込まれ、SetItemAttribute が実行されることを確認します。

   > [!NOTE]
   > UI コンテキストで VSPackage を自動読み込みでき <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid> ます。 詳細については、「 [Load vspackage](../extensibility/loading-vspackages.md)」を参照してください。

4. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]メモ帳でプロジェクトファイルを閉じて開きます。 次のように、 \<Author> 値 Tom のタグが表示されます。

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>こちらもご覧ください

- [カスタムツール](../extensibility/internals/custom-tools.md)
