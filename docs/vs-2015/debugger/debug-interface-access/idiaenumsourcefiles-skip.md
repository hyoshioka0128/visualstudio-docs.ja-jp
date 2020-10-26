---
title: 'IDiaEnumSourceFiles:: Skip |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Skip method
ms.assetid: 4821e6dd-d33f-403d-857d-e3ae81e4a9e3
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 14bfe8762d914770dd2523a431bada883d003511
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189761"
---
# <a name="idiaenumsourcefilesskip"></a>IDiaEnumSourceFiles::Skip
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列挙シーケンス内の指定された数のソースファイルをスキップします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Skip (   
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 celt  
 からスキップする列挙シーケンス内のソースファイルの数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返します。 `S_OK` それ以外の場合は、 `S_FALSE` スキップするソースファイルがない場合はを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
