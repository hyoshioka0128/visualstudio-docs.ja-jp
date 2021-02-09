---
title: ワークフローデザイナー-型コレクションエディター] ダイアログボックス
description: '[型コレクションエディター] ダイアログボックスを使用して、送信および受信アクティビティに既知の型を追加する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b8f194ee792f2a60df71a78af6f41e45aaac91da
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875264"
---
# <a name="type-collection-editor-dialog-box"></a>[型コレクション エディター] ダイアログ ボックス

[ **型コレクションエディター** ] ダイアログボックスを使用すると、既知の型を **送信** および **受信** アクティビティに追加できます。 このダイアログは、 **InvokeMethod** アクティビティにジェネリック型引数を追加するためにも使用されます。 [**型コレクションエディター** ] ダイアログボックスを使用して、既知の型を追加する **送信** アクティビティと **受信** アクティビティには、型の追加が一意である必要があります。 重複する種類が追加され、 **[OK]** をクリックして変更がコミットされた場合は、エラーメッセージが返されます。 [**型コレクションエディター** ] ダイアログボックスで、ジェネリック型引数を追加するために **InvokeMethod** アクティビティに使用すると、重複する型を追加できます。

詳細については、「 [データコントラクトの既知の型](/dotnet/framework/wcf/feature-details/data-contract-known-types)」を参照してください。

次の表では、[ **型コレクション** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|-|-----------------|
|**型リスト**|追加または削除された型のリスト。|

## <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>Send アクティビティおよび Receive アクティビティの [型コレクション エディター] を表示するには

1. [デザイン] ビューで、[ **送信** ] または [ **受信** ] アクティビティを選択します。

2. **F4** キーを押して、[**プロパティ**] ウィンドウを表示します。

3. [ **プロパティ** ] ウィンドウで、 **knowntypes** プロパティの横にある省略記号ボタンをクリックします。

## <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>InvokeMethod アクティビティの [型コレクション エディター] を表示するには

1. デザインビューで [ **InvokeMethod** ] アクティビティを選択します。

2. **F4** キーを押して、[**プロパティ**] ウィンドウを表示します。

3. [ **プロパティ** ] ウィンドウで、 **GenericTypeArguments** プロパティの横にある省略記号ボタンをクリックします。
