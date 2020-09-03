---
title: メッセージ コード | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- message codes
ms.assetid: 9f91f4e2-c1f1-4349-9f11-2fbbf59654be
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 92cc911b0217a406302553b3d913c032fc915b4c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182963"
---
# <a name="message-codes"></a>メッセージ コード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[メッセージ ビュー](../debugger/messages-view.md) に表示される各メッセージ行には、'P'、'S'、's'、または 'R' コードが含まれています。 これらのコードには、次の意味があります。  
  
|コード|説明|  
|----------|-------------|  
|P|**PostMessage** 関数により、メッセージがキューに投稿されました。 メッセージの最終的な処理に関する情報はありません。|  
|S|**SendMessage** 関数により、メッセージが送信されました。 これは、受信側がメッセージを処理して返すまで、送信側は再度制御できるようにならないことを意味します。 このため、受信側は戻り値を送信側に渡すことができます。|  
|s|メッセージは送信されましたが、セキュリティにより、戻り値にアクセスできません。|  
|R|各 'S' 行には、対応する 'R' (リターン) 行があります。これは、メッセージの戻り値の一覧を表示します。 メッセージの呼び出しが入れ子になっている場合があります。これは、あるメッセージ ハンドラーが別のメッセージを送信することを意味します。|
