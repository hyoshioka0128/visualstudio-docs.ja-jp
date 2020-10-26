---
title: Visual Studio API を使用して UML モデルを開く |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, opening models in Visual Studio
ms.assetid: 38423682-f2a7-4d2a-a2cd-fd680e9b4b4d
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 694f10fb0af440513331aa6e76dbf9a59a16d340
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668508"
---
# <a name="open-a-uml-model-by-using-the-visual-studio-api"></a>Visual Studio API を使用して UML モデルを開く
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

API を使って、Visual Studio のユーザー インターフェイスでモデルと図を開くこともできます。

 モデルをユーザーに表示せずに、プログラム コードでモデルの読み込みのみを行う場合は、次の方法を使用できます。

- Visual Studio モデル バスでは、モデルおよびモデル内の要素にアクセスすることができ、あるモデルと別のモデル間のリンクを生成する標準的な方法が提供されます。 詳細については、「 [UML モデルを他のモデルおよびツールと統合](../modeling/integrate-uml-models-with-other-models-and-tools.md)する」を参照してください。

- 読み取り専用モードでモデルを開くことができます。 詳細については、「 [プログラムコードで UML モデルを読み取る](../modeling/read-a-uml-model-in-program-code.md)」を参照してください。

## <a name="opening-models-and-diagrams-in-visual-studio"></a><a name="Showing"></a> Visual Studio でモデルと図を開く
 ユーザー インターフェイスでモデルを開くには、標準の Visual Studio API `EnvDTE.DTE` を使用します。 モデリング プロジェクト項目に対して実行できる便利なキャストが 2 つあります。

- `EnvDTE.Project``IModelingProject`プロジェクトがモデリングプロジェクトであり、プロジェクトが現在の AppDomain に読み込まれている場合は、との間でキャストできます。

- 項目が UML 図の場合、`EnvDTE.ProjectItem` と `IDiagramContext` との間でキャストを行うことができます。

  以降の例の場合、プロジェクトは次の参照をインポートする必要があります。

- EnvDTE

- Microsoft.VisualStudio.ArchitectureTools.Extensibility

- Microsoft.VisualStudio.Modeling.Sdk.[バージョン]

- Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[バージョン]

- Microsoft.VisualStudio.Shell.Immutable.[バージョン]

- Microsoft.VisualStudio.Uml.Interfaces

- System.ComponentModel.Composition

  この例では、Visual Studio で UML モデルを開きます。

```
using EnvDTE; // Visual Studio API for loading diagrams
using
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   // for ICommandExtension and other handler types
using Microsoft.VisualStudio.Uml.Classes;
   // for basic UML types
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   // for model construction methods
using EnvDTE;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
                             // for IDiagram
...
```

 Visual Studio 拡張では、以下の宣言を行うことで、ホスト サービス プロバイダーへのアクセス権を取得できます。

```
[Import] public Microsoft.VisualStudio.Shell.SVsServiceProvider ServiceProvider {get;set;}
...
```

 メソッドで、プロジェクト (たとえば、現在のプロジェクト) にアクセスできます。

```
DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
Project project = dte.ActiveDocument.ProjectItem.ContainingProject;
IModelingProject modelingProject = project as IModelingProject;
if (modelingProject == null) return; // not a modeling project

// Access the model's store and contents.
IModelStore store = modelingProject.Store;
foreach (IElement element in store.Root.OwnedElements) {...}

// Open all the project's diagrams.
foreach (ProjectItem item in project.ProjectItems)
{
     IDiagramContext modelingItem = item as IDiagramContext;
     if (modelingItem == null)
         continue; // not a model diagram
     IDiagram diagram = modelingItem.CurrentDiagram;
     if (diagram == null)
     {
        // Diagram is closed. Open it.
        item.Open().Activate();
        diagram = modelingItem.CurrentDiagram;
     }
     // Access the shapes.
     foreach (IShape<IElement> shape
               in diagram.GetChildShapes<IElement>())
     {
       IElement displayedElement = shape.Element;
       ...
     }
   }
}
```

## <a name="see-also"></a>参照
 [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md) [uml モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)
