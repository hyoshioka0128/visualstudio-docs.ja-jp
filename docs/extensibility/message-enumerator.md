---
title: メッセージ列挙子 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- message enumerator
- source control plug-ins, message enumeration
ms.assetid: 4a4faa0d-d352-40ea-a21d-c09ea286a8e1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0e09b72bd228839268cffc228dd0dc503cc82bd9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80702510"
---
# <a name="message-enumerator"></a>メッセージ列挙子
関数には次のフラグが使用されます `TEXTOUTPROC` 。これは、 [Sccopenproject](../extensibility/sccopenproject-function.md) を呼び出すときに IDE が提供するコールバック関数です (コールバック関数の詳細については、「 [lptextoutproc](../extensibility/lptextoutproc.md) 」を参照してください)。

 IDE からプロセスのキャンセルが求められた場合、キャンセルメッセージの1つが表示されることがあります。 この場合、ソース管理プラグインはを使用して、 `SCC_MSG_STARTCANCEL` IDE に **[キャンセル** ] ボタンを表示するように指示します。 その後、通常のメッセージのセットが送信される可能性があります。 これらのいずれかがを返した場合、 `SCC_MSG_RTN_CANCEL` プラグインは操作を終了し、を返します。 また、プラグインは定期的にポーリングして、 `SCC_MSG_DOCANCEL` ユーザーが操作を取り消したかどうかを判断します。 すべての操作が完了した場合、またはユーザーがキャンセルした場合は、プラグインによってが送信され `SCC_MSG_STOPCANCEL` ます。 `SCC_MSG_INFO`、SCC_MSG_WARNING、および SCC_MSG_ERROR の種類は、メッセージのスクロールリストに表示されるメッセージに使用されます。 `SCC_MSG_STATUS` は、テキストがステータスバーまたは一時的な表示領域に表示されることを示す特殊な型です。 リスト内に永続的に残されているわけではありません。

## <a name="syntax"></a>構文

```
enum { 
   SCC_MSG_RTN_CANCEL = -1, 
   SCC_MSG_RTN_OK = 0, 
   SCC_MSG_INFO = 1 
   SCC_MSG_WARNING, 
   SCC_MSG_ERROR, 
   SCC_MSG_STATUS, 
   SCC_MSG_DOCANCEL, 
   SCC_MSG_STARTCANCEL, 
   SCC_MSG_STOPCANCEL 
};
```

## <a name="members"></a>メンバー
 キャンセルを示すには SCC_MSG_RTN_CANCEL コールバックから戻ります。

 SCC_MSG_RTN_OK コールバックから戻って続行します。

 SCC_MSG_INFO メッセージは情報です。

 SCC_MSG_WARNING メッセージは警告です。

 SCC_MSG_ERROR メッセージはエラーです。

 SCC_MSG_STATUS メッセージはステータスバー用です。

 SCC_MSG_DOCANCEL テキストを表示しません。IDE `SCC_MSG_RTN_OK` はまたはを返し `SCC_MSG_RTN_CANCEL` ます。

 SCC_MSG_STARTCANCEL はキャンセルループを開始します。

 SCC_MSG_STOPCANCEL キャンセルループを停止します。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
