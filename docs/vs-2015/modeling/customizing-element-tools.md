---
title: 要素ツールのカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6dac48b6-db68-4bcd-8aa2-422c2ad5d28b
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b6b35bbb0592f7ec9f8defcd9d78dbba5a6a47a5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655022"
---
# <a name="customizing-element-tools"></a>要素ツールのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL 定義によっては、単一の概念を要素のグループとして表すことができます。 たとえば、コンポーネントに固定のポートセットがあるモデルを作成する場合は、その親コンポーネントと同時にポートを作成することをお勧めします。 したがって、要素作成ツールをカスタマイズして、要素のグループを1つだけではなく作成するようにする必要があります。 これを実現するには、要素作成ツールの初期化方法をカスタマイズします。

 また、ツールを図または要素にドラッグしたときの動作をオーバーライドすることもできます。

## <a name="customizing-the-content-of-an-element-tool"></a>要素ツールのコンテンツのカスタマイズ
 各要素ツールは、 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> 1 つまたは複数のモデル要素とリンクのシリアル化されたバージョンを含む (EGP) のインスタンスを格納します。 既定では、要素ツールの EGP には、ツールに指定したクラスのインスタンスが1つ含まれています。 これを変更するには、*言語*をオーバーライドし `ToolboxHelper.CreateElementToolPrototype` ます。 このメソッドは、DSL パッケージが読み込まれるときに呼び出されます。

 メソッドのパラメーターは、DSL 定義で指定したクラスの ID です。 目的のクラスを使用してメソッドを呼び出すと、EGP に追加の要素を追加できます。

 EGP には、1つのメイン要素から子会社の要素へのリンクを埋め込む必要があります。 参照リンクを含めることもできます。

 次の例では、main 要素と2つの埋め込み要素を作成します。 Main クラスは、"抵抗" と呼ばれ、ターミナルという名前の要素に対する2つの埋め込みリレーションシップを持ちます。 埋め込みロールプロパティの名前は Terminal1 と Terminal2 であり、どちらも 1 ..1 の多重度を持ちます。

```
using Microsoft.VisualStudio.Modeling; ...
public partial class CircuitDiagramToolboxHelper
{
  protected override ElementGroupPrototype    CreateElementToolPrototype(Store store, Guid domainClassId)
  {
    // A case for each tool to customize:
    if (domainClassId == Resistor.DomainClassId)
    {
      // Set up the prototype elements and links:
      Resistor resistor = new Resistor(store);
      resistor.Terminal1 = new Terminal(store);
      resistor.Terminal2 = new Terminal(store);
      resistor.Terminal1.Name = "T1"; // embedding
      resistor.Terminal2.Name = "T2"; // embedding
      // We could also set up reference links.

      // Create an element group prototype for the toolbox:
      ElementGroup egp = new ElementGroup(store.DefaultPartition);
      egp.AddGraph(resistor, true);
      // We do not have to explicitly include embedded children.
      return egp.CreatePrototype();
    }
    // Element tools for other classes:
    else
      return base.CreateElementToolPrototype(store, domainClassId);
  }
}
```

## <a name="see-also"></a>参照
 [要素作成処理および要素移動処理のカスタマイズ](../modeling/customizing-element-creation-and-movement.md)
