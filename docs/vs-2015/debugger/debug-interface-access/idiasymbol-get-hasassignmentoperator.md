---
title: 'IDiaSymbol:: get_hasAssignmentOperator |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasAssignmentOperator method
ms.assetid: fb1acb9c-4500-4343-a590-0395789e4040
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 318229dfdef0bd20048b287e7973c05a40879250
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842232"
---
# <a name="idiasymbolget_hasassignmentoperator"></a>IDiaSymbol::get_hasAssignmentOperator
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザー定義データ型に代入演算子が定義されているかどうかを示すフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_hasAssignmentOperator (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力 `TRUE` ユーザー定義データ型に代入演算子が定義されている場合はを返します。それ以外の場合はを返し `FALSE` ます。  
  
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
