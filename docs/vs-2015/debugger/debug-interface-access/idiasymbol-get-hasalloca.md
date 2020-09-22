---
title: 'IDiaSymbol:: get_hasAlloca |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasAlloca method
ms.assetid: 3b9fb747-670b-4da7-bb70-612f7b911786
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce10647737a34caf3f566ba4f50a84a51ea4c46f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841629"
---
# <a name="idiasymbolget_hasalloca"></a>IDiaSymbol::get_hasAlloca
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

関数に `alloca` (スタックにメモリを割り当てるために使用される) の呼び出しが含まれているかどうかを指定するフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
[C++]HRESULT get_hasAlloca(   BOOL *pFlag);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pFlag`  
 入出力 `TRUE` 関数にへの呼び出しが含まれている場合はを返します。 `alloca` それ以外の場合はを返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="requirements"></a>要件  
  
|要件|説明|  
|-----------------|-----------------|  
|ヘッダー:|dia2|  
|バージョン:|DIA SDK v1.0|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
