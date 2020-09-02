---
title: '[型コレクションエディター] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dae99166b8b811df75f2e2777d176e6778b60c7d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670157"
---
# <a name="type-collection-editor-dialog-box"></a>[型コレクション エディター] ダイアログ ボックス
[ **型コレクションエディター** ] ダイアログボックスを使用すると、既知の型を **送信** および **受信** アクティビティに追加できます。 このダイアログは、 **InvokeMethod** アクティビティにジェネリック型引数を追加するためにも使用されます。 [**型コレクションエディター** ] ダイアログボックスを使用して、既知の型を追加する**送信**アクティビティと**受信**アクティビティには、型の追加が一意である必要があります。 重複する種類が追加され、 **[OK]** をクリックして変更がコミットされた場合は、エラーメッセージが返されます。 [**型コレクションエディター** ] ダイアログボックスで、ジェネリック型引数を追加するために**InvokeMethod**アクティビティに使用すると、重複する型を追加できます。

> [!NOTE]
> [!INCLUDE[crabout](../includes/crabout-md.md)] 、「 [Data Contract Known Types](https://msdn.microsoft.com/library/1a0baea1-27b7-470d-9136-5bbad86c4337)が含まれます。

 次の表では、[ **型コレクション** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**型リスト**|追加または削除された型のリスト。|

## <a name="to-bring-up-the-type-collection-editor"></a>[型コレクション エディター] を表示するには

#### <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>Send アクティビティおよび Receive アクティビティの [型コレクション エディター] を表示するには

1. [デザイン] ビューで、[ **送信** ] または [ **受信** ] アクティビティを選択します。

2. **F4**キーを押して、[**プロパティ**] ウィンドウを表示します。

3. [ **プロパティ** ] ウィンドウで、 **knowntypes** プロパティの横にある省略記号ボタンをクリックします。

#### <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>InvokeMethod アクティビティの [型コレクション エディター] を表示するには

1. デザインビューで [ **InvokeMethod** ] アクティビティを選択します。

2. **F4**キーを押して、[**プロパティ**] ウィンドウを表示します。

3. [ **プロパティ** ] ウィンドウで、 **GenericTypeArguments** プロパティの横にある省略記号ボタンをクリックします。