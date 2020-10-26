---
title: 実行時にプロジェクトのサブタイプを確認する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1e3940097ac53255b7bdd2c12c9ccc64605016e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62584906"
---
# <a name="verifying-subtypes-of-a-project-at-run-time"></a>実行時のプロジェクトのサブタイプの確認
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

カスタムプロジェクトのサブタイプに依存する VSPackage には、サブタイプが存在しない場合に適切に失敗するように、そのサブタイプを検索するロジックを含める必要があります。 次の手順は、指定されたサブタイプの存在を確認する方法を示しています。  
  
### <a name="to-verify-the-presence-of-a-subtype"></a>サブタイプが存在するかどうかを確認するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>VSPackage に次のコードを追加して、プロジェクトオブジェクトとソリューションオブジェクトからプロジェクト階層をオブジェクトとして取得します。  
  
    ```  
    EnvDTE.DTE dte;  
    dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));  
  
    EnvDTE.Project project;  
    project = dte.Solution.Projects.Item(1);  
  
    IVsSolution solution;  
    solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));  
  
    IVsHierarchy hierarchy;  
    hierarchy = solution.GetProjectOfUniqueName(project.UniqueName);  
  
    ```  
  
2. 階層をインターフェイスにキャストし <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> ます。  
  
    ```  
    IVsAggregatableProjectCorrected AP;  
    AP = hierarchy as IVsAggregatableProjectCorrected;  
  
    ```  
  
3. を呼び出して、プロジェクトの種類の Guid の一覧を取得し <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> ます。  
  
    ```  
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();  
  
    ```  
  
4. 指定されたサブタイプの GUID の一覧を確認します。  
  
    ```  
    // Replace the string "MyGUID" with the GUID of the subtype.  
    string guidMySubtype = "MyGUID";  
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)  
    {  
        // The specified subtype is present.  
    }  
    ```  
  
## <a name="see-also"></a>参照  
 [プロジェクトのサブタイプ](../extensibility/internals/project-subtypes.md)   
 [プロジェクトのサブタイプのデザイン](../extensibility/internals/project-subtypes-design.md)   
 [プロジェクト サブタイプによって拡張されるプロパティとメソッド](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
