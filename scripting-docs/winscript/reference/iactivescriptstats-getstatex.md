---
title: 'IActiveScriptStats:: GetStatEx |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptStats.GetStatEx
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptStats::GetStatEx
ms.assetid: f526f51d-8ab5-49ef-a8f7-ae0ac1cb46e4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ca7cdb81fd7e228b26bfaa12d45e81335674a74
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576120"
---
# <a name="iactivescriptstatsgetstatex"></a>IActiveScriptStats::GetStatEx
カスタムスクリプトの統計情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetStatEx(  
   REFGUID  guid,  
   ULONG*   pluHi,  
   ULONG*   pluLo  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `guid`  
 から返す統計情報を指定します。 特定の GUID に対応する統計情報のセマンティクスは、完全に定義されたエンジンです。  
  
 `pluHi`  
 入出力統計を表す64ビット符号なし整数の上位32ビット。  
  
 `pluLo`  
 入出力統計を表す64ビット符号なし整数の下位32ビット。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_NOTIMPL`|このメソッドは実装されていません。|  
  
## <a name="remarks"></a>コメント  
 このメソッドを使用すると、カスタムスクリプトエンジンはカスタムホストにとって意味のある統計情報を返すことができます。  
  
> [!NOTE]
> このメソッドは、現在実装されていません。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptStats:: GetStat](../../winscript/reference/iactivescriptstats-getstat.md)   
 [IActiveScriptStats インターフェイス](../../winscript/reference/iactivescriptstats-interface.md)