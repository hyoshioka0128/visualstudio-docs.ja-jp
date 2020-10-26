---
title: LocationType |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 28bcaa626797313f6ea68a17da33ef9ea192a856
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154206"
---
# <a name="locationtype"></a>LocationType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルに含まれる位置情報の種類を示します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum LocationType {   
   LocIsNull,  
   LocIsStatic,  
   LocIsTLS,  
   LocIsRegRel,  
   LocIsThisRel,  
   LocIsEnregistered,  
   LocIsBitField,  
   LocIsSlot,  
   LocIsIlRel,  
   LocInMetaData,  
   LocIsConstant,  
   LocTypeMax  
};  
```  
  
## <a name="elements"></a>要素  
 `LocIsNull`  
 場所情報は使用できません。  
  
 `LocIsStatic`  
 場所は静的です。  
  
 `LocIsTLS`  
 場所はスレッドローカルストレージにあります。  
  
 `LocIsRegRel`  
 場所はレジスタ相対です。  
  
 `LocIsThisRel`  
 Location は `this` -相対です。  
  
 `LocIsEnregistered`  
 場所が登録されています。  
  
 `LocIsBitField`  
 場所はビットフィールドにあります。  
  
 `LocIsSlot`  
 Location は、Microsoft 中間言語 (MSIL) スロットです。  
  
 `LocIsIlRel`  
 場所は MSIL 相対です。  
  
 `LocInMetaData`  
 場所はメタデータ内にあります。  
  
 `LocIsConstant`  
 場所は定数値です。  
  
 `LocTypeMax`  
 この列挙体の場所の種類の数。  
  
## <a name="remarks"></a>注釈  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)インターフェイスで使用できるプロパティは、イメージファイル内のシンボルの場所によって異なります。 詳細については、「 [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」を参照してください。  
  
 この列挙体の値は、 [IDiaSymbol:: get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md) メソッドへの呼び出しによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol:: get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)   
 [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
