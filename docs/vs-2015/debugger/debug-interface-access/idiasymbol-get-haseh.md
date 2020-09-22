---
title: 'IDiaSymbol:: get_hasEH |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasEH method
ms.assetid: 9a4952d8-9fa7-4798-b48c-fe4357648276
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e4badf13f21bae028ee782d23bc26b1c1348ebeb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841817"
---
# <a name="idiasymbolget_haseh"></a>IDiaSymbol::get_hasEH
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

関数にアンマネージ C++ スタイルの例外処理 (try/catch ブロックなど) が含まれているかどうかを指定するフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT get_hasEH(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pFlag`  
 入出力関数に C++ スタイルの例外処理がある場合はを返します。 `TRUE` それ以外の場合はを返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、 `S_FALSE` そのシンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="requirements"></a>要件  
  
|要件|説明|  
|-----------------|-----------------|  
|ヘッダー:|dia2|  
|バージョン:|DIA SDK v1.0|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
