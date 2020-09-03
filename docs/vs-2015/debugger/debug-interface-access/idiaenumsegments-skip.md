---
title: 'IDiaEnumSegments:: Skip |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Skip method
ms.assetid: ec67039f-da8c-4e70-8db7-957d7d5281e8
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1f8f816ef374c827e35b7c208e237b2dbd9384bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189851"
---
# <a name="idiaenumsegmentsskip"></a>IDiaEnumSegments::Skip
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列挙シーケンス内の指定された数のセグメントをスキップします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Skip (   
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 celt  
 からスキップする列挙シーケンス内のセグメントの数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返します。 `S_OK` それ以外の場合は、 `S_FALSE` スキップするセグメントがなくなった場合はを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
