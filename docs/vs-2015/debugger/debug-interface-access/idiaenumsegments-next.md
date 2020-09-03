---
title: 'IDiaEnumSegments:: Next |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Next method
ms.assetid: 53f61874-d821-47ab-a1f5-27e982804a6a
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e00f85d4b3a111f3a68b934006a32197245d4d6e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189874"
---
# <a name="idiaenumsegmentsnext"></a>IDiaEnumSegments::Next
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列挙シーケンス内の指定された数のセグメントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Next (   
   ULONG         celt,   
   IDiaSegment** rgelt,  
   ULONG*        pceltFetched  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 celt  
 から取得する列挙子内のセグメントの数。  
  
 rgelt  
 入出力セグメントを表す目的の [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) オブジェクトを使用して入力する配列。  
  
 pceltFetched  
 入出力フェッチされた列挙子内のセグメントの数を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 これ `S_FALSE` 以上セグメントがない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)   
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
