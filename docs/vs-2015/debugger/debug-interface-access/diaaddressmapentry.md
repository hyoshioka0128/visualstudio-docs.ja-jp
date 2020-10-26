---
title: DiaAddressMapEntry |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 67c0a3e297f3eebfbf44724e64c4989d9bb979fb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164355"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

アドレスマップのエントリを記述します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
struct DiaAddressMapEntry {   
   DWORD rva,  
   DWORD rvaTo  
};  
```  
  
## <a name="elements"></a>要素  
 `rva`  
 イメージ A の相対仮想アドレス (RVA)。  
  
 `rvaTo`  
 イメージ B で、相対仮想アドレス `rva` がにマップされます。  
  
## <a name="remarks"></a>注釈  
 アドレスマップは、1つのイメージレイアウト (A) から別のイメージレイアウト (B) への変換を提供します。 `DiaAddressMapEntry`によって並べ替えられた構造体の配列は、 `rva` アドレスマップを定義します。  
  
 イメージ A のアドレスをアドレスに変換するには、 `addrA` `addrB` イメージ B で次の手順を実行します。  
  
1. マップで、 `e` 最大値以下のエントリを検索 `rva` `addrA` します。  
  
2. `delta = addrA – e.rva` を設定します。  
  
3. `addrB = e.rvaTo + delta` を設定します。  
  
   `DiaAddressMapEntry`構造体の配列は、 [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)メソッドに渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: dia2  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
