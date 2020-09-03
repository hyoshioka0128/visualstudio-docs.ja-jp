---
title: プログラムコードで UML モデルを読み取る |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, reading models
ms.assetid: 0f63105e-6079-498a-94f1-318c0f5f9621
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bbc55204987f4b6ea0d45c4228f6c194f1ebaf64
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671304"
---
# <a name="read-a-uml-model-in-program-code"></a>プログラム コードで UML モデルを読み取る
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML API を使用して、UML モデルおよび UML 図を読み込むことができます。

## <a name="reading-a-model-in-program-code"></a><a name="Reading"></a> プログラムコードでのモデルの読み取り
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ウィンドウに表示せずにモデルのコンテンツにアクセスするには、`ModelingProject.LoadReadOnly()` を使用します。

 次に例を示します。

```
using Microsoft.VisualStudio.Uml.Classes;
               // for IElement
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
               // for ModelingProject
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
               // for IModelStore
...
string projectPath = @"C:\MyProjectFolder\MyProject.modelproj";
using (IModelingProjectReader projectReader =
           ModelingProject.LoadReadOnly(projectPath))
{
   IModelStore store = projectReader.Store;
   foreach (IClass umlClass in store.AllInstances<IClass>())
   {
       ...
   }
}
```

 図の中の図形を読み込むには、プロジェクトを読み込んでから図を読み込む必要があります。

 次に例を示します。

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
                             // for IDiagram
...
foreach (string diagramFile in projectReader. DiagramFileNames)
{
  IDiagram diagram = projectReader.LoadDiagram(diagramFile);
  foreach (IShape<IElement> shape
         in diagram.GetChildShapes<IElement>())
  { ... }
}
```

## <a name="alternative-methods"></a>その他の方法
 多くのアプリケーションでは、modelbus を使用すると、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] このトピックで説明する方法よりも堅牢性と柔軟性が高く、モデルと要素を参照することができます。 同じモデル、または別のモデル内の任意の要素をリンクするための、標準的な方法を使用できます。 詳細については、「 [UML モデルを他のモデルおよびツールと統合](../modeling/integrate-uml-models-with-other-models-and-tools.md)する」を参照してください。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API を使用して、ユーザー インターフェイスでモデルおよび図を開くこともできます。 詳細については、「 [Visual STUDIO API を使用して UML モデルを開く](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)」を参照してください。

## <a name="stand-alone-applications"></a><a name="Standalone"></a> スタンドアロンアプリケーション
 前のセクションの例は、Visual Studio 拡張機能で動作します。 スタンドアロン アプリーションでモデルを読み込むこともできますが、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトにいくつかの参照を追加する必要があります。

> [!NOTE]
> スタンドアロン アプリケーションでモデルを読み込む方法については、製品の今後のバージョンで変更される可能性があります。 現在のバージョンで使用できる機能のいくつかは、将来のバージョンでは利用できなくなる可能性があります。

#### <a name="to-add-references-to-read-a-model-in-a-stand-alone-application"></a>スタンドアロン アプリケーションのモデルを読み込むための参照を追加するには

1. ソリューションエクスプローラーで、アプリケーションをビルドするプロジェクトを右クリックし、[ **プロパティ**] をクリックします。 プロパティエディターの [ **アプリケーション** ] タブで、[ **ターゲットフレームワーク** ] を .NET Framework の必要なバージョンに設定します。

2. UML モデルにアクセスするために必要な [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 参照を追加します。

   - Microsoft.VisualStudio.Uml.Interfaces.dll

   - Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll

3. 前のセクションに記載されている参照に加えて、次のプロジェクト参照を、 **\Common7\IDE\PrivateAssemblies Visual Studio [version]** から追加します。

   - Microsoft.VisualStudio.Uml.dll

   - Microsoft.VisualStudio.TeamArchitect.ModelStore.Dsl.dll

     アプリケーションで図を読み込む場合は、次の参照が必要になることもあります。

   - Microsoft.VisualStudio.TeamArchitect.ActivityDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.ComponentDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.LogicalClassDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.SequenceDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.UseCase.Dsl.dll

## <a name="see-also"></a>参照
 [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md) [uml モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)
