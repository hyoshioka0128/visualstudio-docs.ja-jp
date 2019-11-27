---
title: 'IActiveScriptAuthor:: GetEventHandler |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetEventHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetEventHandler
ms.assetid: 87c7a71d-46b9-448c-b34d-394105e20982
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c69b32f0040ea6d52e0712b8e1813cc5a0b40c58
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576230"
---
# <a name="iactivescriptauthorgeteventhandler"></a>IActiveScriptAuthor::GetEventHandler
指定された属性を持つスクリプトレットを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetEventHandler(  
   IDispatch          *pdisp,  
   LPCOLESTR          pszItem,  
   LPCOLESTR          pszSubItem,  
   LPCOLESTR          pszEvent,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdisp`  
 からスクリプトレットがアタッチされる `NamedItem` に対応する `IDispatch` オブジェクト。  
  
 `pszItem`  
 からホストの完全修飾スクリプトレット名の最上位レベル識別子のバッファーアドレス。  
  
 `pszSubItem`  
 からホストの完全修飾スクリプトレット名の第2レベル識別子のバッファーアドレス。 名前にレベルが1つしかない場合は NULL に設定します。  
  
 `pszEvent`  
 からイベント名を格納しているバッファーのアドレス。 スクリプトレットは、このイベントのイベントハンドラーです。  
  
 `ppse`  
 入出力指定された属性を持つスクリプトレットの `IScriptEntry` インターフェイスへのポインターを受け取る変数のアドレス。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IScriptEntry インターフェイス](../../winscript/reference/iscriptentry-interface.md)