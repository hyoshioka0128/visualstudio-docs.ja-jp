---
title: プロジェクト項目に属性を追加する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- attributes [Visual Studio], adding to a project item
ms.assetid: 404a71d5-cce5-44e7-9eaf-d747c794fedb
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1740ac4dfdeb64d5b4b2b0aab264845de9c186dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184820"
---
# <a name="adding-an-attribute-to-a-project-item"></a>プロジェクト項目への属性の追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

メソッドとは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetItemAttribute%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> プロジェクト項目の属性の値を取得および設定します。 SetItemAttribute が存在しない場合は、属性が作成され、プロジェクト項目メタデータに追加されます。  
  
## <a name="adding-an-attribute-to-a-project-item"></a>プロジェクト項目への属性の追加  
  
#### <a name="to-add-an-attribute-to-a-project-item"></a>プロジェクト項目に属性を追加するには  
  
- 次のコードでは、オートメーションオブジェクトとメソッドを使用して、 <xref:EnvDTE.DTE> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> プロジェクト項目に属性を追加しています。 プロジェクト項目 ID は、プロジェクト項目名 "program.cs" から取得されます。 属性 "MyAttribute" がこのプロジェクト項目に追加され、"MyValue" という値が指定されます。  
  
    ```  
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));  
    EnvDTE.Project project = dte.Solution.Projects.Item(1);  
  
    string uniqueName = project.UniqueName;  
    IVsSolution solution =     (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));  
    IVsHierarchy hierarchy;  
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);  
    IVsBuildPropertyStorage buildPropertyStorage = hierarchy as IVsBuildPropertyStorage;  
    if (buildPropertyStorage != null)  
    {  
        uint itemId;  
        string fullPath =         (string)project.ProjectItems.Item("Program.cs").Properties.Item("FullPath").Value;  
        hierarchy.ParseCanonicalName(fullPath, out itemId);  
        buildPropertyStorage.SetItemAttribute(  
            itemId, "MyAttribute", "MyValue");  
    }  
  
    ```  
  
## <a name="see-also"></a>参照  
 [MSBuild プロジェクト ファイルでのデータの保持](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
