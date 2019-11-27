---
title: 'IDebugApplication:: HandleRuntimeError |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.HandleRuntimeError
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::HandleRuntimeError
ms.assetid: f8f3bbaf-09e5-4d01-8a35-f380bc7ff8ed
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2fd4ba2b811cd6c4e38c10a0c68c5808f2c0870a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574332"
---
# <a name="idebugapplicationhandleruntimeerror"></a>IDebugApplication::HandleRuntimeError
現在のスレッドをブロックし、エラーの通知をデバッガー IDE に送信します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT HandleRuntimeError(  
   IActiveScriptErrorDebug*  pErrorDebug,  
   IActiveScriptSite*        pScriptSite,  
   BREAKRESUMEACTION*        pbra,  
   ERRORRESUMEACTION*        perra,  
   BOOL*                     pfCallOnScriptError  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pErrorDebug`  
 から発生したエラー。  
  
 `pScriptSite`  
 からスレッドのスクリプトサイト。  
  
 `pbra`  
 入出力デバッガーがアプリケーションを再開したときに実行するアクション。  
  
 `perra`  
 入出力デバッガーがエラーが発生した場合にアプリケーションを再開したときに実行するアクション。  
  
 `pfCallOnScriptError`  
 入出力エンジンが `IActiveScriptSite::OnScriptError` メソッドを呼び出す必要がある場合に `TRUE` するフラグ。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 言語エンジンは、実行時エラーの原因となったスレッドのコンテキストでこのメソッドを呼び出します。 このメソッドにより、現在のスレッドがブロックされ、デバッガー IDE に送信されるエラー通知が送信されます。 デバッガー IDE によってアプリケーションが再開されると、このメソッドは、実行するアクションと共にを返します。  
  
> [!NOTE]
> ランタイムエラーが発生している間に、スタックフレームの列挙や式の評価などのタスクを実行するために、スレッドによって言語エンジンが呼び出される場合があります。  
  
## <a name="see-also"></a>参照  
 [IDebugApplication インターフェイス](../../winscript/reference/idebugapplication-interface.md)   
 [IActiveScriptErrorDebug インターフェイス](../../winscript/reference/iactivescripterrordebug-interface.md)   
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)   
 [BREAKRESUMEACTION 列挙型](../../winscript/reference/breakresumeaction-enumeration.md)   
 [ERRORRESUMEACTION 列挙型](../../winscript/reference/errorresumeaction-enumeration.md)