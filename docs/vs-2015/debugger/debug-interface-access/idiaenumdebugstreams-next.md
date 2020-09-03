---
title: 'IDiaEnumDebugStreams:: Next |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Next method
ms.assetid: eb8eae5a-be27-45f4-a7bd-6e4ef0652385
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d25b7cf505f0aa049d0faceb093599a1cd0b78cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182597"
---
# <a name="idiaenumdebugstreamsnext"></a>IDiaEnumDebugStreams::Next
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列挙シーケンス内の指定された数のデバッグストリームを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Next (   
   ULONG                     celt,   
   IDiaEnumDebugStreamData** rgelt,  
   ULONG*                    pceltFetched  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 celt  
 から取得する列挙子内のデバッグストリームの数。  
  
 rgelt  
 入出力取得するデバッグストリームを表す [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md) オブジェクトの配列を返します。  
  
 pceltFetched  
 入出力返されたデバッグストリームの数を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 ストリームがなくなっ `S_FALSE` た場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)
