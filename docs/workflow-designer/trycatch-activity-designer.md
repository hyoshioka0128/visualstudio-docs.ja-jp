---
title: ワークフローデザイナー-TryCatch アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TryCatch.UI
- System.Activities.Statements.Catch`1.UI
ms.assetid: 02a326c2-4009-442f-b7cb-e42121fd2992
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b70f1d3174990ec12c621dff4a45ce4d899ceb4e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593071"
---
# <a name="trycatch-activity-designer"></a>TryCatch アクティビティ デザイナー

**TryCatch**アクティビティデザイナーは、<xref:System.Activities.Statements.TryCatch> アクティビティを作成および構成するために使用されます。

## <a name="the-trycatch-activity"></a>TryCatch アクティビティ
 <xref:System.Activities.Statements.TryCatch> アクティビティには、<xref:System.Activities.Statements.TryCatch.Try%2A> アクティビティ、 **Catch\<TException >** のコレクション、および <xref:System.Activities.Statements.TryCatch.Finally%2A> アクティビティが含まれています。 **Texception**型の <xref:System.Activities.Statements.Catch%601> には、<xref:System.Activities.Statements.Catch%601.ExceptionType%2A> と <xref:System.Activities.Statements.Catch%601.Action%2A>が含まれています。 これらの組み合わせによって、標準的な例外ベースのエラー処理機構が実装されます。 <xref:System.Activities.Statements.TryCatch> アクティビティは、対応する <xref:System.Activities.Statements.TryCatch.Try%2A> アクティビティの実行を試みます。 <xref:System.Activities.Statements.TryCatch.Try%2A> アクティビティが例外をスローした場合、<xref:System.Activities.Statements.TryCatch> アクティビティはその**Catch < TException\>** コレクションを使用して例外を照合します。 一致するものがある場合は、対応する**Catch\<TException >** の <xref:System.Activities.Statements.Catch%601.Action%2A> が実行され、例外のエラー処理ロジックとして機能します。 <xref:System.Activities.Statements.TryCatch.Try%2A> セクションのアクティビティまたは <xref:System.Activities.Statements.TryCatch.Catches%2A> のアクティビティが正常に完了した場合、<xref:System.Activities.Statements.TryCatch> アクティビティは <xref:System.Activities.Statements.TryCatch.Finally%2A> アクティビティを実行します。 詳細については、「 [Windows workflow exceptions](/dotnet/framework/windows-workflow-foundation/exceptions)」を参照してください。

### <a name="using-the-trycatch-activity-designer"></a>TryCatch アクティビティ デザイナーの使用

**[ツールボックス]** の **[エラー処理]** カテゴリで、 **TryCatch**アクティビティデザイナーにアクセスします。

**TryCatch**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置している任意の場所 (<xref:System.Activities.Statements.Sequence>内など) にドロップしてワークフローデザイナー画面にドロップできます。 この操作により、TryCatch の既定の <xref:System.Activities.Statements.TryCatch> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> 値は、 **TryCatch**アクティビティデザイナーのヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。 その他のプロパティは、 **TryCatch**アクティビティデザイナーの画面で編集する必要があります。

**TryCatch**デザイナーの右上隅にある展開ボタンをクリックすると、展開ビューの **[Try]** 、 **[Catch]** 、および **[Finally]** の各ボックスが表示されます。 キャッチを追加するには、 **TryCatch**デザイナーの **[新しい catch の追加]** ボタンをクリックします。 このボタンが、型のコンボ ボックスに変化します。 例外の型を選択し、Enter キーを押して catch を追加します。 キャッチを追加する**と、catch**領域が展開され、catch にアクティビティをドロップして catch の実行ロジックを定義できます。 展開された catch 領域の右側にはテキスト ボックスが表示されます。 このテキスト ボックスを使用して、例外変数に名前を付けることができます。 例外変数は、同じ**Catch**内のアクティビティに対してのみ使用できます。

**TryCatch**デザイナーは、 **Catch**の編集をサポートしていません。 例外の種類を変更する場合は、**キャッチ**を削除して新しいものを追加する必要があります。 キャッチを削除するには、**キャッチ**を選択して削除するか、右クリックによってアクセスされるコンテキストメニューの **[削除]** を選択します。

### <a name="the-trycatch-properties"></a>TryCatch のプロパティ

次の表は、<xref:System.Activities.Statements.TryCatch>のプロパティと、デザイナーでのそれらの使用方法を示しています。

|プロパティ名|必須|使用状況|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|[False]|<xref:System.Activities.Statements.TryCatch> アクティビティの表示名を指定します (省略可能)。 既定値は TryCatch です。|
|<xref:System.Activities.Statements.TryCatch.Try%2A>|[False]|<xref:System.Activities.Statements.TryCatch> を実行すると、このアクティビティが最初に実行されます。|
|<xref:System.Activities.Statements.TryCatch.Catches%2A>|[False]|<xref:System.Activities.Statements.TryCatch.Try%2A> アクティビティが例外をスローした場合にチェックされる**Catch**要素のコレクション。<br /><br /> <xref:System.Activities.Statements.TryCatch.Catches%2A> にアクティビティを少なくとも 1 つ追加するか、または、<xref:System.Activities.Statements.TryCatch.Finally%2A> ブロックにアクティビティを追加する必要があります。|
|<xref:System.Activities.Statements.TryCatch.Finally%2A>|[False]|<xref:System.Activities.Statements.TryCatch.Try%2A> および <xref:System.Activities.Statements.TryCatch.Catches%2A> コレクション内の必要なアクティビティがすべて完了した段階で実行されるアクティビティ。<br /><br /> <xref:System.Activities.Statements.TryCatch.Catches%2A> にアクティビティを少なくとも 1 つ追加するか、または、<xref:System.Activities.Statements.TryCatch.Finally%2A> ブロックにアクティビティを追加する必要があります。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [Rethrow](../workflow-designer/rethrow-activity-designer.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
