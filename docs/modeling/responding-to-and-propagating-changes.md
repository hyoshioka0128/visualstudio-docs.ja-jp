---
title: 変更内容への対応および変更内容の反映
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7c51aeea4a1637e5b1b9d2de0d8b92920334e2fc
ms.sourcegitcommit: ba966327498a0f67d2df2291c60b62312f40d1d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "93414517"
---
# <a name="respond-to-and-propagate-changes"></a>応答と変更の反映

要素を作成、削除、または更新すると、モデルの他の部分に変更を反映するコード、またはファイル、データベース、その他のコンポーネントなどの外部リソースに変更を反映するコードを記述できます。

## <a name="reference"></a>リファレンス

ガイドラインとして、これらの手法を次の順序で検討します。

|手法|シナリオ|詳細情報|
|-|-|-|
|計算されるドメインプロパティを定義します。|モデル内の他のプロパティから計算された値を持つドメインプロパティ。 たとえば、関連する要素の価格の合計である価格です。|[計算プロパティおよびカスタム格納プロパティ](../modeling/calculated-and-custom-storage-properties.md)|
|カスタムストレージドメインプロパティを定義します。|モデルの他の部分または外部に格納されているドメインプロパティ。 たとえば、式文字列をモデル内のツリーに解析することができます。|[計算プロパティおよびカスタム格納プロパティ](../modeling/calculated-and-custom-storage-properties.md)|
|OnValueChanging や OnDeleting などの変更ハンドラーのオーバーライド|異なる要素を同期したままにして、外部の値をモデルと同期させます。<br /><br /> 定義された範囲に値を制限します。<br /><br /> プロパティ値およびその他の変更の直前と直後に呼び出されます。 例外をスローすることによって、変更を終了できます。|[ドメイン プロパティ値変更ハンドラー](../modeling/domain-property-value-change-handlers.md)|
|ルール|変更が発生したトランザクションの終了の直前に、実行のためにキューに登録されているルールを定義できます。 これらは、Undo または Redo では実行されません。 それらを使用して、ストアの1つの部分を別のストアと同期させます。|[規則によって変更内容がモデル内に反映される](../modeling/rules-propagate-changes-within-the-model.md)|
|ストアイベント|モデリングストアは、要素またはリンクの追加や削除、プロパティの値の変更などのイベントの通知を提供します。 このイベントは、Undo および Redo でも実行されます。 ストアイベントを使用して、ストアに含まれていない値を更新します。|[イベント ハンドラーによって変更内容がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)|
|.NET イベント|図形には、マウスのクリックやその他のジェスチャに応答するイベントハンドラーがあります。 各オブジェクトについて、これらのイベントに登録する必要があります。 通常、登録は InitializeInstanceResources のオーバーライドで行われ、各要素に対して実行する必要があります。<br /><br /> これらのイベントは、通常、トランザクションの外部で発生します。|[方法: シェイプまたはデコレーターに対するクリック操作を受け取る](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|
|境界ルール|境界規則は、図形の境界を制限するために特に使用されます。|[BoundsRules によってシェイプの位置とサイズが制限される](/previous-versions/visualstudio/visual-studio-2015/modeling/boundsrules-constrain-shape-location-and-size?preserve-view=true&view=vs-2015)|
|選択ルール|選択規則は、ユーザーが選択できる内容を限定します。|[方法: 現在の選択項目を表示および制限する](../modeling/how-to-access-and-constrain-the-current-selection.md)|
|OnAssocatedPropertyChanged|図形とコネクタの特徴 (影、矢印、色、線の幅、スタイルなど) を使用して、モデル要素の状態を示します。|[シェイプおよびコネクタの更新とモデルへの反映](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|

## <a name="compare-rules-and-store-events"></a>ルールとストアイベントの比較

変更 notifiers、ルール、およびイベントは、モデルで変更が発生したときに実行されます。

通常、ルールは、変更が発生した最後のトランザクションで適用され、トランザクションの変更がコミットされた後にイベントが適用されます。

ストアイベントを使用して、モデルをストアの外部のオブジェクトと同期し、ストア内の一貫性を維持するルールを使用します。

- **カスタムルールの作成** 派生クラスとして、抽象ルールからカスタムルールを作成します。 また、カスタム規則についてフレームワークに通知する必要があります。 詳細については、「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

- **サブスクライブ (イベントを** )イベントをサブスクライブする前に、イベントハンドラーとデリゲートを作成します。 次に、プロパティを使用して <xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A> 、イベントをサブスクライブします。 詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

- **変更を元に戻す** トランザクションを元に戻すと、イベントが発生しますが、ルールは適用されません。 規則によって値が変更され、その変更を元に戻すと、元に戻す操作中に値が元の値にリセットされます。 イベントが発生した場合は、値を元の値に手動で変更する必要があります。 トランザクションと元に戻す方法の詳細については、「 [方法: トランザクションを使用](../modeling/how-to-use-transactions-to-update-the-model.md)してモデルを更新する」を参照してください。

- **ルールとイベントへのイベント引数の引き渡し** イベントとルールの両方に `EventArgs` 、モデルがどのように変更されたかに関する情報を含むパラメーターが渡されます。

## <a name="see-also"></a>関連項目

- [方法: シェイプまたはデコレーターに対するクリック操作を受け取る](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)
- [Domain-Specific 言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)