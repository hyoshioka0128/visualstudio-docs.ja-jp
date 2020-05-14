---
title: メッセージ列挙子 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702510"
---
# <a name="message-enumerator"></a>メッセージ列挙子
次のフラグは、関数に`TEXTOUTPROC`使用されます。 [SccOpenProject](../extensibility/sccopenproject-function.md) [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)

 IDE がプロセスをキャンセルするように求められた場合、キャンセル メッセージのいずれかが表示されることがあります。 この場合、ソース管理プラグインは IDE に`SCC_MSG_STARTCANCEL` **[キャンセル]** ボタンを表示するように要求するために使用します。 この後、通常のメッセージのセットが送信される可能性があります。 これらのいずれかが返された`SCC_MSG_RTN_CANCEL`場合、プラグインは操作を終了し、戻ります。 また、プラグインは定期的に`SCC_MSG_DOCANCEL`ポーリングを行い、ユーザーが操作をキャンセルしたかどうかを判断します。 すべての操作が完了した場合、またはユーザーがキャンセルした場合、プラグインは を送信`SCC_MSG_STOPCANCEL`します。 メッセージ`SCC_MSG_INFO`のスクロール リストに表示されるメッセージには、メッセージの種類、SCC_MSG_WARNING、およびSCC_MSG_ERRORが使用されます。 `SCC_MSG_STATUS`は、テキストがステータス バーまたは一時的な表示領域に表示されることを示す特殊な型です。 リストに永続的に残りません。

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
 SCC_MSG_RTN_CANCEL コールバックから戻ってキャンセルを示します。

 SCC_MSG_RTN_OK コールバックから戻って続行します。

 SCC_MSG_INFO メッセージは情報提供です。

 SCC_MSG_WARNING メッセージは警告です。

 SCC_MSG_ERROR メッセージはエラーです。

 SCC_MSG_STATUS メッセージはステータス バー用です。

 SCC_MSG_DOCANCEL テキストなし。IDE`SCC_MSG_RTN_OK`は`SCC_MSG_RTN_CANCEL`、 または を返します。

 SCC_MSG_STARTCANCEL キャンセル ループを開始します。

 SCC_MSG_STOPCANCELキャンセル ループを停止します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
