---
title: ワークフローデザイナー- &lt; T &gt; アクティビティデザイナーの切り替え
description: Switch アクティビティデザイナーを使用して <T> 、ワークフローデザイナーで switch アクティビティを作成および構成する方法について説明し <T> ます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.ModelItemKeyValuePair.UI
- System.Activities.Statements.Switch`1.UI
ms.assetid: 18a6c96e-49a9-4356-ab61-fbd7e3ab44bb
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f6bdf05878c08b1c175b78ff2205b74c4ea5669b
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94433935"
---
# <a name="switcht-activity-designer"></a>Switch\<T> アクティビティ デザイナー

<xref:System.Activities.Statements.Switch%601> アクティビティは、指定した式を評価します。そして、その評価から得られた値と一致する、関連付けられたキーを持つアクティビティを、アクティビティのコレクションから実行します。

**スイッチ<T \>** アクティビティデザイナーは、ワークフローデザイナーでアクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Switch%601> ます。

## <a name="the-switchtactivity"></a>Switch \<T> アクティビティ

<xref:System.Activities.Statements.Switch%601> アクティビティには、<xref:System.Activities.Statements.Switch%601.Expression%2A> と、<xref:System.Activities.Statements.Switch%601.Cases%2A> のディクショナリが含まれます。 ディクショナリ内の各ケースは、 *キー* と、対応する *値* として機能するアクティビティを含むペアで構成されます。 <xref:System.Activities.Statements.Switch%601> アクティビティは、<xref:System.Activities.Statements.Switch%601.Expression%2A> を評価し、それを各キーと比較します。 一致が見つかった場合は、対応するアクティビティが実行されます。 見つかる一致は 1 つのみです。これは、ディクショナリ キーは、ディクショナリの等値比較子により定義される等価性の型に従って一意である必要があるためです。 一致が検出されない場合は、<xref:System.Activities.Statements.Switch%601.Default%2A> アクティビティが実行されます。

## <a name="how-to-use-the-switcht-activity-designer"></a>Switch アクティビティデザイナーの使用方法 \<T>

[ **ツールボックス** ] の [ **制御フロー** ] カテゴリにある **\<T> Switch** アクティビティデザイナーにアクセスします。 ワークフローデザイナーにドロップすると、 **[型の選択** ] ダイアログボックスが表示され、アクティビティで使用されるジェネリック型 *T* をユーザーが指定できるように <xref:System.Activities.Statements.Switch%601> なります。 既定値は **Int32** です。 ジェネリック型 *t* を選択すると、 **スイッチ<t \>** デザイナーがワークフローデザイナーに追加されます。

次に示すのは、 **スイッチ<\> T** デザイナーのプロパティです。 これらのプロパティはすべて、プロパティ グリッドで編集できます。 一部のプロパティは、デザイナー画面で設定することもできます。

次の表に、最も役に立つ <xref:System.Activities.Statements.Switch%601> プロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Switch%601> アクティビティ デザイナーの表示名を指定します。 既定値は Switch<Int32 \> です。 この値は、[ **プロパティ** ] ウィンドウで編集することも、デザイナーヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Switch%601.Expression%2A>|○|cases コレクション内のキーを比較して、実行する case を決定するために使用される式を指定します。|
|<xref:System.Activities.Statements.Switch%601.Default%2A>||一致が検出されなかった場合に実行するアクティビティを指定します。 デザイナーの [ **アクティビティの追加** ] ボタンをクリックして、アクティビティをドロップできる **既定** のボックスを開きます。|
|<xref:System.Activities.Statements.Switch%601.Cases%2A>||評価する case を指定します。 ケースを追加するには、 **スイッチ \<T>** デザイナーの下部にある [ **新しいケースの追加** ] ボタンをクリックします。 ボタンがテキストボックスに変わります (スイッチの追加時に選択されたジェネリック型が String または Enum である場合は、コンボボックスに \<T> なります)。 [ **ケースの値** ] ボックスにキーを追加すると、ケース領域が展開され、"ここにアクティビティをドロップします" というヒントテキストが表示されたら、ケースの実行ロジックを定義します。|

case キーが重複しない限り、複数の case を追加できます。 case キーが重複している場合は、エラー ダイアログが表示され、指定した case キーが既に存在しているために別のキーを選択する必要があることが示されます。 **スイッチ \<T>** デザイナーでは、一度に1つのケース領域だけを展開ビューに配置できます。 折りたたまれたビューに case の領域が表示されている場合は、case の領域をクリックすると展開されます。 case が折りたたまれており、この case 内にアクティビティが存在する場合は、このアクティビティの表示名が右側に表示されます。 それ以外の場合は、[ **アクティビティの追加** ] ボタンが表示され、クリックするとケースが展開され、アクティビティを追加できるようになります。

既存の case のキーをクリックすると、キーがラベルからテキスト ボックスに変わり、case キーを編集できます。

case を削除する方法には、次の 2 つがあります。

- case を選択して削除します。

- ケースを選択し、右クリックしてコンテキストメニューを表示し、[ **削除** ] を選択します。

case を削除するには、case 自体を選択する必要があることに注意してください。 case 内のアクティビティを選択して削除すると、case ではなく、アクティビティのみが削除されます。

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
