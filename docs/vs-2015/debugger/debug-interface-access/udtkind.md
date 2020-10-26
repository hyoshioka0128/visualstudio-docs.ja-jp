---
title: UdtKind |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- UdtKind enumeration
ms.assetid: 400b59b9-373c-42cb-aae1-570494214328
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9fb22471cea7cd717b8969682a0e1f643f912150
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202378"
---
# <a name="udtkind"></a>UdtKind
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

さまざまなユーザー定義型 (UDT) について説明します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum UdtKind {   
   UdtStruct,  
   UdtClass,  
   UdtUnion,  
   UdtInterface  
};  
```  
  
## <a name="elements"></a>要素  
 UdtStruct  
 UDT は構造体です。  
  
 UdtClass  
 UDT はクラスです。  
  
 UdtUnion  
 UDT は共用体です。  
  
 UdtInterface  
 UDT はインターフェイスです。  
  
## <a name="remarks"></a>注釈  
 この列挙体の値は、 [IDiaSymbol:: get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md) メソッドによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)
