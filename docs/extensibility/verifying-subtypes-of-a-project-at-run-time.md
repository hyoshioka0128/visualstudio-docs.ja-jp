---
title: 実行時にプロジェクトのサブタイプを確認する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f0d739a9f8734dd8941e3254d03364cbf4c77350
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698181"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>実行時にプロジェクトのサブタイプを確認する
カスタムプロジェクトのサブタイプに依存する VSPackage には、サブタイプが存在しない場合に適切に失敗するように、そのサブタイプを検索するロジックを含める必要があります。 次の手順は、指定されたサブタイプの存在を確認する方法を示しています。

### <a name="to-verify-the-presence-of-a-subtype"></a>サブタイプが存在するかどうかを確認するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>VSPackage に次のコードを追加して、プロジェクトオブジェクトとソリューションオブジェクトからプロジェクト階層をオブジェクトとして取得します。

    ```csharp
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

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. を呼び出して、プロジェクトの種類の Guid の一覧を取得し <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> ます。

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. 指定されたサブタイプの GUID の一覧を確認します。

    ```csharp
    // Replace the string "MyGUID" with the GUID of the subtype.
    string guidMySubtype = "MyGUID";
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)
    {
        // The specified subtype is present.
    }
    ```

## <a name="see-also"></a>関連項目
- [プロジェクトのサブタイプ](../extensibility/internals/project-subtypes.md)
- [プロジェクトのサブタイプのデザイン](../extensibility/internals/project-subtypes-design.md)
- [プロジェクトのサブタイプによって拡張されたプロパティとメソッド](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
