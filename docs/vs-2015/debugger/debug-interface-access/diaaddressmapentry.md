---
title: DiaAddressMapEntry |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa2824b7fbd10e7628e5c6b0a016615620933df9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756248"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

アドレス マップ内のエントリについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
struct DiaAddressMapEntry {   
   DWORD rva,  
   DWORD rvaTo  
};  
```  
  
## <a name="elements"></a>Elements  
 `rva`  
 A. イメージの相対仮想アドレス (RVA)  
  
 `rvaTo`  
 相対仮想アドレス`rva`B. イメージ内にマップされます  
  
## <a name="remarks"></a>Remarks  
 アドレス マップは、(A) をもう 1 つ (B) 1 つのイメージのレイアウトからの翻訳を提供します。 配列の`DiaAddressMapEntry`構造体の順に並べ替えて`rva`アドレス マップを定義します。  
  
 アドレスに変換する`addrA`、イメージ アドレス内`addrB`B の図で、次の手順に従います。  
  
1. マップのエントリを検索`e`が大きいもの`rva`に等しいまたはそれよりも小さい`addrA`します。  
  
2. 設定`delta = addrA – e.rva`します。  
  
3. 設定`addrB = e.rvaTo + delta`します。  
  
   配列の`DiaAddressMapEntry`に構造体が渡される、 [idiaaddressmap::set_addressmap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)メソッド。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: dia2.h  
  
## <a name="see-also"></a>関連項目  
 [列挙体と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)



