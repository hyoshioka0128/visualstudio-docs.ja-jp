---
title: Uml API を使用して UML シーケンス図を編集する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML activity diagrams, programming
ms.assetid: 8cdd0203-85ef-4c62-9abc-da4cb26fa504
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cbc7a6ce7edede6759c0562df1e524d932f62b91
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669709"
---
# <a name="edit-uml-sequence-diagrams-by-using-the-uml-api"></a>UML API を使用して UML シーケンス図を編集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

相互作用とは、一連の生存線の間におけるメッセージのシーケンスです。 相互作用は、UML シーケンス図に表示されます。

 API の詳細については、「 [VisualStudio](/previous-versions/dd493373(v=vs.140))」を参照してください。

 UML 図のコマンドとジェスチャハンドラーの記述に関する一般的な概要については、「 [モデリング図でのメニューコマンドの定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)」を参照してください。

## <a name="basic-code"></a>基本コード

### <a name="namespace-imports"></a>名前空間インポート
 次の `using` ステートメントを含める必要があります。

```
using Microsoft.VisualStudio.Uml.Classes;
   // for basic UML types such as IPackage
using Microsoft.VisualStudio.Uml.Interactions;
   // for interaction types
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   // to create elements and use additional functions
```

 メニュー コマンドおよびジェスチャ ハンドラーを作成する場合は、次も必要です。

```
using System.ComponentModel.Composition;
   // for Import and Export
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   // for ICommandExtension
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
   // for diagrams and context
```

 詳細については、「 [モデリング図のメニューコマンドの定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)」を参照してください。

### <a name="getting-the-context"></a>コンテキストの取得
 相互作用を、シーケンス図のコマンドまたはジェスチャ ハンドラーの一部として編集している場合、コンテキストへの参照を取得できます。 次に例を示します。

```
[SequenceDesignerExtension]
[Export(typeof(ICommandExtension))]
public class MySequenceDiagramCommand : ICommandExtension
{
    [Import]
    public IDiagramContext Context { get; set; }
    public void QueryStatus (IMenuCommand command)
    {
      ISequenceDiagram sequenceDiagram =
          Context.CurrentDiagram as ISequenceDiagram;
         ...
```

### <a name="generated-and-uml-sequence-diagrams"></a>生成されるシーケンス図と UML シーケンス図
 シーケンス図には 2 種類あります。1 つは UML モデリング プロジェクトで手動で作成するシーケンス図、もう 1 つはプログラム コードから生成されるシーケンス図です。 シーケンス図の種類を判断するには、`UmlMode` プロパティを使用します。 

> [!NOTE]
> このプロパティは、Visual Studio 2013 またはそれ以前のバージョンを使用したコードから生成されたシーケンス図の場合のみ、false を返します。 これには、Visual Studio 2013 またはそれ以前のバージョンから移行されたコード生成型シーケンスが含まれます。 このバージョンの Visual Studio では、新しいシーケンス図の生成をサポートしていません。

 たとえば、UML シーケンス図でのみ表示できるメニュー コマンドを生成する場合、`QueryStatus()` メソッドに次のステートメントを含めることができます。

```
command.Enabled = command.Visible =
      sequenceDiagram != null && sequenceDiagram.UmlMode;
```

 生成されたシーケンス図では、生存線、メッセージ、その他の要素は、UML シーケンス図の場合とほぼ同じように表示されます。 UML モデルでは、モデル ストアにルートがあり、このルートがその他のすべての要素を所有するモデルになります。 一方、生成された相互作用はそれ自体のモデル ストアに存在しており、これには次の null ルートが設定されます。

```
IModel rootModel = sequenceDiagram.ModelStore.Root;
    // !sequenceDiagram.UmlMode == (rootModel == null)
```

## <a name="to-create-and-display-an-interaction"></a>相互作用を作成して表示するには
 相互作用をパッケージまたはモデルの子として作成します。

 たとえば、空のシーケンス図で実行される可能性があるコマンドを開発する場合、相互作用が存在するかどうかを確認するところから始める必要があります。

```
public void Execute (IMenuCommand command)
{
    ISequenceDiagram sequenceDiagram =
         Context.CurrentDiagram as ISequenceDiagram;
    if (sequenceDiagram == null) return;
    // Get the diagram's interaction:
    IInteraction interaction = sequenceDiagram.Interaction;
    // A new sequence diagram might have no interaction:
    if (interaction == null)
    {
       // Get the home package or model of the diagram:
       IPackage parentPackage = sequenceDiagram.GetObject<IPackage>();
       interaction = parentPackage.CreateInteraction();
       // Display the interaction on the sequence diagram:
       sequenceDiagram.Bind(interaction);
    }
```

## <a name="updating-an-interaction-and-its-layout"></a>相互作用とそのレイアウトの更新
 相互作用を更新する場合、必ず次のいずれかのメソッドを使用してレイアウトを更新することによって操作を終了する必要があります。

- `ISequenceDiagram.UpdateShapePositions()` 最近挿入または移動された図形と、隣接する図形の位置を調整します。

- `ISequenceDiagram.Layout([SequenceDiagramLayoutKinds])` ダイアグラム全体を再描画します。 パラメーターを使用して、生存線、メッセージ、またはその両方の再配置を指定できます。

  これは特に、新規の要素を挿入する場合、または既存の要素を移動する場合に重要です。 これらのいずれかの操作を実行しなければ、図上で正しく配置されません。 必要な処理は、一連の変更の最後に、これらの操作のいずれかを 1 回呼び出すことだけです。

  コマンドを実行した後に、元に戻す操作を実行したユーザーが混乱しないよう、`ILinkedUndoTransaction` を使用し、変更と最終的な `Layout()` または `UpdateShapePositions()` 操作を囲みます。 次に例を示します。

```
using (ILinkedUndoTransaction transaction = LinkedUndoContext.BeginTransaction("create loop"))
{
  Interaction.CreateCombinedFragment(InteractionOperatorKind.Loop, messages);
  Diagram.UpdateShapePositions();
  transaction.Commit();
}
```

 `ILinkedUndoTransaction` を使用するには、クラス内で次の宣言を行う必要があります。

```
[Import] ILinkedUndoContext LinkedUndoContext { get; set; }
```

 詳細については、「 [トランザクションを使用した UML モデルの更新のリンク](../modeling/link-uml-model-updates-by-using-transactions.md)」を参照してください。

## <a name="building-an-interaction"></a>相互作用の構築

### <a name="to-create-lifelines"></a>生存線を生成するには

```
ILifeline lifeline = interaction.CreateLifeline();
```

 生存線は、接続可能要素、つまり型のインスタンスを表します。 たとえば、コンポーネントが受信メッセージをどのように内部パートに渡すかを相互作用を使用して示す場合、生存線はコンポーネントのポートとパートを表すことができます。

```
foreach (IConnectableElement part in
            component.Parts
           .Concat<IConnectableElement>(component.OwnedPorts))
{
   ILifeline lifeline = interaction.CreateLifeline();
   lifeline.Represents = part;
}
```

 または、相互作用で任意のオブジェクトのセットを表す場合、相互作用自体にプロパティまたはその他の `IConnectableElement` を作成することもできます。

```
ILifeline lifeline = interaction.CreateLifeline();
IProperty property1 = interaction.CreateProperty();
property1.Type = model.CreateInterface();
property1.Type.Name = "Type 1";
lifeline.Represents = property1;
```

 さらに別の方法として、接続可能要素にリンクせずに、生存線の名前と型を設定することもできます。

```
ILifeline lifeline = interaction.CreateLifeline();
lifeline.Name = "c1";
lifeline.SetInstanceType("Customer");
System.Diagnostics.Debug.Assert(
           lifeline.GetDisplayName() == "c1:Customer"  );
```

### <a name="to-create-messages"></a>メッセージを作成するには
 メッセージを作成するには、ソースの生存線およびターゲットの生存線での挿入ポイントを特定する必要があります。 次に例を示します。

```
interaction.CreateMessage( sourceInsertionPoint,
                           targetInsertionPoint,
                           MessageKind.Complete,
                           MessageSort.ASynchCall)
```

 ソースまたはターゲットが定義されていないメッセージを作成するには、次のようにします。

```
interaction.CreateLostFoundMessage(MessageKind.Found, insertionPoint);
```

 生存線のすべてのキー ポイントで挿入ポイントを特定するために使用できるメッセージを次の表に示します。

|ILifeline のメソッド|挿入ポイント|
|-------------------------|------------------------------------|
|`FindInsertionPointAtTop()`|生存線の上部|
|`FindInsertionPointAtBottom()`|生存線の下部|
|`FindInsertionPointAfterMessage`<br /><br /> `(IMessage previous)`|指定されたメッセージの直後のポイント|
|`FindInsertionPointAfterExecutionSpecification`<br /><br /> `(IExecutionSpecification previous)`|生存線上、または親の実行指定ブロック上のポイント|
|`FindInsertionPointAfterInteractionUse`<br /><br /> `(IInteractionUse previous)`|相互作用使用に続くポイント|
|`FindInsertionPointAfterCombinedFragment`<br /><br /> `(ICombinedFragment previous)`|結合フラグメントに続くポイント|
|`FindInsertionPoint(IExecutionSpecification block)`|実行ブロックの上部|
|`FindInsertionPoint(IInteractionOperand fragment)`|結合フラグメントのオペランドの上部|

 メッセージを作成する場合は、別のメッセージと重複するメッセージを定義しないように注意してください。

### <a name="to-create-combined-fragments-and-interaction-uses"></a>結合フラグメントおよび相互作用使用を作成するには
 要素の範囲に含まれる生存線それぞれに挿入位置を指定することにより、結合フラグメントおよび相互作用使用を作成できます。 既存のメッセージやフラグメントと重複するポイントを指定しないように注意してください。

```
Interaction.CreateCombinedFragment(InteractionOperatorKind.Loop,
  Interaction.Lifelines.Select(lifeline => lifeline.FindInsertionPointAtTop()));
Interaction.CreateInteractionUse(
  Interaction.Lifelines.Select(lifeline => lifeline.FindInsertionPointAtTop()));
```

 また、既存のメッセージ セットを処理する結合フラグメントも作成できます。 メッセージは、すべて同じ生存線または実行ブロックから供給される必要があります。

```
ICombinedFragment cf = Interaction.CreateCombinedFragment(
  InteractionOperatorKind.Loop,
  Interaction.Lifelines.First().GetAllOutgoingMessages());
```

 結合フラグメントは、常に単一のオペランドで生成されます。 新しいオペランドを作成するには、前か後に挿入する既存のオペランドを指定すると共に、それを後に挿入するか、前に挿入するかを指定する必要があります。

```
// Create an additional operand before the first
cf.CreateInteractionOperand(cf.Operands.First(), false);
// Create an additional operand after the last:
cf.CreateInteractionOperand(cf.Operands.Last(), true);
```

## <a name="troubleshooting"></a>トラブルシューティング
 変更が `UpdateShapePositions()` または `Layout()` 操作で完了していない場合、図形は誤った位置に表示されます。

 その他のほとんどの問題は、挿入位置がずれているために、新規メッセージまたはフラグメントが他のメッセージやフラグメントと重複することになるために発生します。 この場合、変更が実行されない、または例外がスローされるという症状が見られます。 例外は、`UpdateShapePositions()` または `Layout()` 操作が実行されるまではスローされないことがあります。

## <a name="see-also"></a>関連項目

- [VisualStudio (相互作用)](/previous-versions/dd493373(v=vs.140))
- [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)
- [モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
- [カスタム モデリング ツールボックス アイテムを定義する](../modeling/define-a-custom-modeling-toolbox-item.md)
- [UML モデルの検証制約を定義する](../modeling/define-validation-constraints-for-uml-models.md)
- [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md)
