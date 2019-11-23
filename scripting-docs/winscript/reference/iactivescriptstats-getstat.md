---
title: 'IActiveScriptStats:: GetStat |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptStats.GetStat
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptStats::GetStat
ms.assetid: 31fd15b3-0713-4b55-b4f7-bfd7ea198493
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 096f1cf5b9bf8b5533bd5c36d33f014c747ff9aa
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574334"
---
# <a name="iactivescriptstatsgetstat"></a>IActiveScriptStats::GetStat
標準スクリプト統計の1つを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetStat(  
   DWORD   stid,  
   ULONG*  pluHi,  
   ULONG*  pluLo  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `stid`  
 から返す統計情報を指定します。 次の値である必要があります。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|SCRIPTSTAT_STATEMENT_COUNT|1|スクリプトが開始された後、または統計がリセットされた後に実行されたステートメントの数を返します。|  
  
 `pluHi`  
 入出力統計を表す64ビット符号なし整数の上位32ビット。  
  
 `pluLo`  
 入出力統計を表す64ビット符号なし整数の下位32ビット。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 使用できる値は次のとおりです。ただし、次の表の値には制限されません。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、標準スクリプト統計の1つを返します。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptStats:: GetStatEx](../../winscript/reference/iactivescriptstats-getstatex.md)   
 [IActiveScriptStats インターフェイス](../../winscript/reference/iactivescriptstats-interface.md)