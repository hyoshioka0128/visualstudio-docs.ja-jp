---
title: BasicType |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- BasicType enumeration
ms.assetid: 19ae53ba-cd6e-47b6-9f94-27ae663ce955
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 38de89b9774ac20f67b91e4ba864534122f4cdb0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580838"
---
# <a name="basictype"></a>BasicType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルの基本型を指定します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum BasicType {   
   btNoType   = 0,  
   btVoid     = 1,  
   btChar     = 2,  
   btWChar    = 3,  
   btInt      = 6,  
   btUInt     = 7,  
   btFloat    = 8,  
   btBCD      = 9,  
   btBool     = 10,  
   btLong     = 13,  
   btULong    = 14,  
   btCurrency = 25,  
   btDate     = 26,  
   btVariant  = 27,  
   btComplex  = 28,  
   btBit      = 29,  
   btBSTR     = 30,  
   btHresult  = 31  
};  
```  
  
## <a name="elements"></a>要素  
 btNoType  
 基本型が指定されていません。  
  
 btVoid  
 基本型は `void` です。  
  
 btChar  
 基本型は、 `char` (C/c + + 型) です。  
  
 btWChar  
 基本型はワイド (Unicode) 文字 ( `WCHAR` ) です。  
  
 btInt  
 基本型は `signed int` (C/c + + 型) です。  
  
 btUInt  
 基本型は `unsigned int` (C/c + + 型) です。  
  
 btFloat  
 基本型は浮動小数点数 ( `FLOAT` ) です。  
  
 btBCD  
 基本型は、バイナリでコード化された10進数 ( `BCD` ) です。  
  
 btBool  
 基本型はブール値 ( `BOOL` ) です。  
  
 btLong  
 基本型は、 `long int` (C/c + + 型) です。  
  
 btULong  
 基本型は `unsigned long int` (C/c + + 型) です。  
  
 btCurrency  
 基本型は currency です。  
  
 btDate  
 基本型は date/time ( `DATE` ) です。  
  
 btVariant  
 基本型は変数型の構造体 ( `VARIANT` ) です。  
  
 btComplex  
 基本型は複素数です。  
  
 btBit  
 基本型はビットです。  
  
 btBSTR  
 基本型は、基本またはバイナリ文字列 ( `BSTR` ) です。  
  
 btHresult  
 基本型は `HRESULT` です。  
  
## <a name="remarks"></a>注釈  
 この列挙体の値は、 [IDiaSymbol:: get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md) メソッドによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol:: get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)   
 [IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)
