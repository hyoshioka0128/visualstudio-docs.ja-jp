---
title: 'IActiveScript:: SetScriptState |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.SetScriptState
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_SetScriptState
ms.assetid: f2b2700c-0c8d-40db-ad84-dc751c5d9bc2
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea947e00ffd5a3498261f4a3a8acd4791e8ace60
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577988"
---
# <a name="iactivescriptsetscriptstate"></a>IActiveScript::SetScriptState
指定された状態にスクリプトエンジンを配置します。 このメソッドは非ベースのスレッドから呼び出すことができます。この場合、非ベースのコールアウトによってオブジェクトをホストするか、 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)インターフェイスを使用することはできません。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetScriptState(  
    SCRIPTSTATE ss  // identifier of new state  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ss`  
 からスクリプトエンジンを特定の状態に設定します。 [Scriptstate 列挙](../../winscript/reference/scriptstate-enumeration.md)型に定義されている値のいずれかを指定できます。  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの値を返します。  
  
|戻り値|意味|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_FAIL`|スクリプトエンジンは、初期化された状態への移行をサポートしていません。 ホストは、このスクリプトエンジンを破棄し、同じ効果を得るために新しいスクリプトエンジンを作成、初期化、および読み込みする必要があります。|  
|`E_UNEXPECTED`|呼び出しは想定されていませんでした (たとえば、スクリプトエンジンがまだ読み込まれていないか初期化されていないため)。そのため失敗しました。|  
|`OLESCRIPT_S_PENDING`|メソッドは正常にキューに登録されましたが、状態はまだ変更されていません。 状態が変化すると、 [IActiveScriptSite:: OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)メソッドを使用してサイトがコールバックされます。|  
|`S_FALSE`|メソッドは成功しましたが、スクリプトは既に指定された状態にあります。|  
  
## <a name="remarks"></a>コメント  
 スクリプトエンジンの状態の詳細については、「 [Windows スクリプト](../../winscript/windows-script-engines.md)エンジン」の「スクリプトエンジンの状態」セクションを参照してください。  
  
## <a name="see-also"></a>参照  
 [IActiveScript:: Clone](../../winscript/reference/iactivescript-clone.md)   
 [IActiveScript:: GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)   
 [IActiveScript:: InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)   
 [IActiveScriptParse::P arsescripttext](../../winscript/reference/iactivescriptparse-parsescripttext.md)   
 [IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)