---
title: ワークフロー デザイナーでのエラー メッセージ
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- WFDErrorMessages.UI
- System.Activities.Presentation.ErrorActivity.UI
- System.Activities.Presentation.View.ErrorView.UI
ms.assetid: 4d8bbc2e-34fc-477f-9140-4adfd70c34a0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 72592d21fdaba1ef47a15a113c820dffe0ba71eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75597049"
---
# <a name="error-messages-in-workflow-designer"></a>ワークフロー デザイナーでのエラー メッセージ

このトピックでは、ワークフローデザイナーを操作するときに発生する可能性のあるエラーメッセージの種類について説明します。

## <a name="situations-in-which-errors-in-the-workflow-designer-occur"></a>ワークフロー デザイナーでエラーが発生する状況

ワークフローデザイナーのエラーは、次の状況で発生します。

1. 式でエラーが発生している。

2. アクティビティの検証制約が満たされていない。

3. アクティビティによる読み込み失敗を引き起こすエラーが XAML ファイルで発生している。

4. ワークフローによる読み込み失敗を引き起こすエラーが XAML ファイルで発生している。

無効な式や検証制約違反によって、ワークフローの構築が失敗することはありません。 ワークフローのビルドは成功しますが、 <xref:System.Activities.InvalidWorkflowException> 実行時にがスローされます。 XAML ファイルにエラーがある場合は、構築が失敗します。

Visual Studio 内では、ワークフローが読み込まれると、そのエラーが **エラー一覧**に表示されます。 エラーの原因となっているアクティビティに移動するには、 **エラー一覧**でエラーをダブルクリックします。

### <a name="expression-errors"></a>式のエラー
 無効な式が赤い円で示され、その式の横に白い感嘆符が付いています。 このアイコンの上にカーソルを置くと、エラーの原因を表すツールヒントが表示されます。 Visual Studio 内で式をクリックすると、エラーの原因を示す行が表示されます。 下線が引かれたテキストの上にカーソルを置くと、エラーの発生元を示すツールヒントが表示されます。

### <a name="activity-validation-errors"></a>アクティビティ検証エラー
 アクティビティの検証制約に違反する場合は、赤い円と白い感嘆符がアクティビティの右上角に表示されます。 このアイコンの上にカーソルを置くと、エラーの原因を表すツールヒントが表示されます。

### <a name="xaml-load-errors"></a>XAML 読み込みエラー
 アクティビティの読み込みに失敗すると、"XAML でエラーが発生したため、アクティビティを読み込むことができませんでした" というテキストの赤いボックスが表示されます。 これは通常、アクティビティの型を解決できない場合に発生します。 デザイナーで赤いボックスを選択して、それを削除すると、無効なアクティビティを削除できます。

### <a name="workflow-load-errors"></a>ワークフロー読み込みエラー
 ワークフローの読み込みに失敗すると、デザイナー画面にワークフローデザイナー "ドキュメントで問題が発生しました" というテキストと、ワークフローの読み込みに失敗した原因となった例外情報が表示されます。 通常、これは、XAML ファイルを解析できない場合に発生します。
