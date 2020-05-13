---
title: プロジェクト項目への属性の追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- attributes [Visual Studio], adding to a project item
ms.assetid: 404a71d5-cce5-44e7-9eaf-d747c794fedb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 059eef0b6a215f1f02c77df63f777fbfda5dff19
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740192"
---
# <a name="add-an-attribute-to-a-project-item"></a>プロジェクト項目に属性を追加する
メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetItemAttribute%2A>と取得<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A>し、プロジェクト項目の属性の値を設定します。 SetItemAttribute は、存在しない場合は、プロジェクト項目のメタデータに追加する属性を作成します。

## <a name="add-an-attribute-to-a-project-item"></a>プロジェクト項目に属性を追加する

- 次のコードでは、<xref:EnvDTE.DTE>オートメーション オブジェクトと<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A>メソッドを使用して、プロジェクト項目に属性を追加します。 プロジェクト項目 ID は、プロジェクト項目名 "program.cs" から取得されます。 属性 "MyAttribute" はこのプロジェクト項目に追加され、"MyValue" という値が与えられます。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    IVsBuildPropertyStorage buildPropertyStorage = hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item("Program.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "MyAttribute", "MyValue");
    }

    ```

## <a name="see-also"></a>関連項目
- [MSBuild プロジェクト ファイルにデータを保存する](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
