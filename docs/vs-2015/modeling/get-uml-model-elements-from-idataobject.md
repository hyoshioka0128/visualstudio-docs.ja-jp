---
title: IDataObject | から UML モデル要素を取得するMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, copy and paste
ms.assetid: e0b9cec8-3b93-4a24-8bd3-3e086501d387
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 66b4ffc312af89aa5852a1f4dad62fd328176df3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72666084"
---
# <a name="get-uml-model-elements-from-idataobject"></a>IDataObject から UML モデル要素を取得する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザーが任意のソースから要素を UML 図にドラッグすると、ドラッグされた要素は `System.Windows.Forms.IDataObject` でエンコードされます。 エンコーディングは、ソース オブジェクトの種類によって決まります。 次のフラグメントでは、ソースが UML 図である場合に要素をどのように取得するかについて示します。

> [!NOTE]
> UML モデルに対して実行する必要がある操作のほとんどは、アセンブリ **VisualStudio** と **VisualStudio**で定義されている型を使用して実行できます。また、 しかし、そのためには、UML モデリング ツールの実装の一部であるいくつかのクラスを使用する必要があります。 たとえば、このフラグメントの `ShapeElement` は UML の `IShape` と同じではありません。 UML モデルと図が不整合な状態になる可能性を低くするには、他に方法がない場合を除き、これらの実装クラスに対してメソッドを使用しないことをお勧めします。

## <a name="code-sample"></a>コード サンプル
 プロジェクトは、次のアセンブリを参照する必要があり [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] ます。

 **Microsoft.VisualStudio.Modeling.Sdk.[バージョン]**

 **Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[バージョン]**

 **System.Windows.Forms**

```
using Microsoft.VisualStudio.Modeling;
  // for ElementGroupPrototype
using Microsoft.VisualStudio.Modeling.Diagrams;
  // for ShapeElement, DiagramDragEventArgs, DiagramPointEventArgs
… 
  /// <summary>
  /// Retrieves UML IElements from drag arguments.
  /// Works for drags from UML diagrams.
  /// </summary>
  private IEnumerable<IElement> GetModelElementsFromDragEvent
                  (DiagramDragEventArgs dragEvent)
  {
     //ElementGroupPrototype is the container for
     //dragged and copied elements and toolbox items.
     ElementGroupPrototype prototype =
        dragEvent.Data.
        GetData(typeof(ElementGroupPrototype))
                     as ElementGroupPrototype;
     // Locate the originals in the implementation store.
     IElementDirectory implementationDirectory =
        dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;

     return  prototype.ProtoElements.Select(
       prototypeElement =>
       {
          ModelElement element = implementationDirectory
                .FindElement(prototypeElement.ElementId);
          ShapeElement shapeElement = element as ShapeElement;
          if (shapeElement != null)
          {
            // Dragged from a diagram.
            return shapeElement.ModelElement as IElement;
          }
          else
          {
            // Dragged from UML Model Explorer.
            return element as IElement;
          }
        });
    }
```

 `ElementGroupPrototype`および UML モデリングツールが実装されているの詳細については `Store` 、「[モデリング SDK for Visual Studio-ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)」を参照してください。

## <a name="see-also"></a>参照
 [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md)[モデリング図にメニューコマンドを定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)する
