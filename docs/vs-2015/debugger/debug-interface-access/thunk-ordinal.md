---
title: THUNK_ORDINAL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b98098c0b6e1de9c3c2ceda5c644bc2957ab22bd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62576409"
---
# <a name="thunk_ordinal"></a>THUNK_ORDINAL
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

サンクの種類を指定します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
typedef enum THUNK_ORDINAL {   
   THUNK_ORDINAL_NOTYPE,  
   THUNK_ORDINAL_ADJUSTOR,  
   THUNK_ORDINAL_VCALL,  
   THUNK_ORDINAL_PCODE,  
   THUNK_ORDINAL_LOAD   
  
   // trampoline thunk ordinals - only for use in Trampoline thunk symbols  
   THUNK_ORDINAL_TRAMP_INCREMENTAL,  
   THUNK_ORDINAL_TRAMP_BRANCHISLAND,  
} THUNK_ORDINAL;  
```  
  
## <a name="elements"></a>要素  
 THUNK_ORDINAL_NOTYPE  
 標準サンク。  
  
 THUNK_ORDINAL_ADJUSTOR  
 `this`Adjustor サンク。  
  
 THUNK_ORDINAL_VCALL  
 仮想呼び出しサンク。  
  
 THUNK_ORDINAL_PCODE  
 P-コードサンク。  
  
 THUNK_ORDINAL_LOAD  
 遅延読み込みサンク。  
  
 THUNK_ORDINAL_TRAMP_INCREMENTAL  
 インクリメンタル trampoline サンク (trampoline サンクは、あるメモリ領域から別のメモリ領域への呼び出しをバウンスするために使用されます)。  
  
 THUNK_ORDINAL_TRAMP_BRANCHISLAND  
 分岐点 trampoline サンク。  
  
## <a name="remarks"></a>注釈  
 この列挙体の値は、 [IDiaSymbol:: get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md) メソッドの呼び出しから返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)
