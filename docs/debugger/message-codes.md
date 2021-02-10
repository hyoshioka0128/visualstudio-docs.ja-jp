---
title: メッセージ コード | Microsoft Docs
description: メッセージ ビューの各メッセージ行に表示されるメッセージ コードの意味について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- message codes
ms.assetid: 9f91f4e2-c1f1-4349-9f11-2fbbf59654be
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 92562dda3e8a705d2cdf9b00561aa13cbd9d75e5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891775"
---
# <a name="message-codes"></a>メッセージ コード
[メッセージ ビュー](../debugger/messages-view.md) に表示される各メッセージ行には、'P'、'S'、's'、または 'R' コードが含まれています。 これらのコードには、次の意味があります。

|コード|説明|
|----------|-------------|
|P|**PostMessage** 関数により、メッセージがキューに投稿されました。 メッセージの最終的な処理に関する情報はありません。|
|S|**SendMessage** 関数により、メッセージが送信されました。 これは、受信側がメッセージを処理して返すまで、送信側は再度制御できるようにならないことを意味します。 このため、受信側は戻り値を送信側に渡すことができます。|
|s|メッセージは送信されましたが、セキュリティにより、戻り値にアクセスできません。|
|R|各 'S' 行には、対応する 'R' (リターン) 行があります。これは、メッセージの戻り値の一覧を表示します。 メッセージの呼び出しが入れ子になっている場合があります。これは、あるメッセージ ハンドラーが別のメッセージを送信することを意味します。|