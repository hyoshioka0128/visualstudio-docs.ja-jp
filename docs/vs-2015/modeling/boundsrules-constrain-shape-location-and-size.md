---
title: BoundsRules 制約図形の位置とサイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
ms.assetid: 4d08e541-fc67-4e68-bf31-30d346aa2aa0
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7d660189ede0848216eb44d6ef49fe9c93a06ec8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672725"
---
# <a name="boundsrules-constrain-shape-location-and-size"></a>BoundsRules によってシェイプの位置とサイズが制限される
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*境界規則*は、図形のサイズと位置に関する制限を定義するクラスです。 ユーザーが図形をドラッグしているとき、または図形の角または辺をドラッグしているときに、繰り返し呼び出されるメソッドを提供します。

 次の例では、四角形の形状を固定サイズのバー (水平または垂直) に制限しています。 ユーザーが角または辺をドラッグすると、[高さ] と [幅] の2つの許可された構成が反転されます。

 境界規則は、から派生したクラスです <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules> 。 ルールのインスタンスは、次のような形で作成されます。

```
using Microsoft.VisualStudio.Modeling.Diagrams; ...
public partial class BarShape
{
  /// <summary>
  /// Rule invoked when the user is resizing a shape.
  /// </summary>
  public override BoundsRules BoundsRules
  { get { return new BarBoundsRule(); } }
}
/// <summary>
/// Rule invoked when the user is changing a shape's outline.
/// Provides real-time mouse rubber-band feedback, so must work fast.
/// </summary>
public class BarBoundsRule: BoundsRules
{
  public override RectangleD GetCompliantBounds
     (ShapeElement shape, RectangleD proposedBounds)
  {
    double thickness = 0.1;
    if (proposedBounds.Height > proposedBounds.Width)
    {
      // There is a minimum width for a shape; the width
      // will actually be set to the lesser of
      // thickness and that minimum.
      return new RectangleD(proposedBounds.Location,
            new SizeD(thickness, proposedBounds.Height));
    }
    else
    {
      // There is a minimum height for a shape; the
      // height will actually be set to the lesser of
      // thickness and that minimum.
      return new RectangleD(proposedBounds.Location,
         new SizeD(proposedBounds.Width, thickness));
} } }
```

 必要に応じて、場所とサイズの両方を制限できることに注意してください。

## <a name="see-also"></a>参照
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules> [変更内容への対応および変更内容の反映](../modeling/responding-to-and-propagating-changes.md)
