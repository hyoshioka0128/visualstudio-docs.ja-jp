---
title: THUNK_ORDINAL |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a92e0fa81bdfc7c33e790c5022c2fbe341d632be
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847711"
---
# <a name="thunkordinal"></a>THUNK_ORDINAL
サンクの種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```C++  
typedef enum THUNK_ORDINAL {   
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
  
## <a name="elements"></a>Elements  
 THUNK_ORDINAL_NOTYPE  
 標準のサンクします。  
  
 THUNK_ORDINAL_ADJUSTOR  
 A`this`サンクの調整権限を保持します。  
  
 THUNK_ORDINAL_VCALL  
 仮想呼び出しサンクします。  
  
 THUNK_ORDINAL_PCODE  
 P コード サンクします。  
  
 THUNK_ORDINAL_LOAD  
 遅延読み込みのサンクします。  
  
 THUNK_ORDINAL_TRAMP_INCREMENTAL  
 増分トランポリン サンクが (1 つのメモリ領域からの呼び出しを間跳ねるトランポリン サンクが使用されます)。  
  
 THUNK_ORDINAL_TRAMP_BRANCHISLAND  
 分岐ポイント トランポリン サンクします。  
  
## <a name="remarks"></a>Remarks  
 この列挙体の値が呼び出しから返される、 [idiasymbol::get_thunkordinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)メソッド。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: cvconst.h  
  
## <a name="see-also"></a>関連項目  
 [列挙体と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)