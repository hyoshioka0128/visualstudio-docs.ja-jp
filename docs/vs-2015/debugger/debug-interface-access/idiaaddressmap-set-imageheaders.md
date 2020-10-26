---
title: IDiaAddressMap::set_imageHeaders | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_imageHeaders method
ms.assetid: a46b9d0e-43e6-433f-b2c7-aa203981e4e4
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 18fa69929f78d5ae661169a09db97697d98f4d94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198637"
---
# <a name="idiaaddressmapset_imageheaders"></a>IDiaAddressMap::set_imageHeaders
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

相対仮想アドレス変換を有効にするためにイメージヘッダーを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT set_imageHeaders (   
   DWORD cbData,  
   BYTE  data[],  
   BOOL  originalHeaders  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 cbData  
 からヘッダーデータのバイト数。 はである必要があり `n*sizeof(IMAGE_SECTION_HEADER)` `n` ます。は実行可能ファイル内のセクションヘッダーの数です。  
  
 data[]  
 から  `IMAGE_SECTION_HEADER` イメージヘッダーとして使用される構造体の配列。  
  
 originalHeaders  
 からアップグレードの `FALSE` 前に元のイメージが反映されている場合は、イメージヘッダーが新しいイメージからのものである場合はに設定し `TRUE` ます。 通常、これは `TRUE` [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) メソッドの呼び出しと組み合わせた場合にのみ設定されます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 `IMAGE_SECTION_HEADER`構造体は、winnt.h で宣言され、実行可能ファイルのイメージセクションヘッダー形式を表します。  
  
 相対仮想アドレスの計算は、値によって異なり `IMAGE_SECTION_HEADER` ます。 通常、DIA は、プログラムデータベース (.pdb) ファイルからこれらを取得します。 これらの値が指定されていない場合、DIA は相対仮想アドレスを計算できず、 [IDiaAddressMap:: get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) メソッドはを返し `FALSE` ます。 次に、クライアントは、 [IDiaAddressMap::p ut_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md) メソッドを呼び出して、イメージ自体から不足しているイメージヘッダーを提供した後に、相対仮想アドレスの計算を有効にする必要があります。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)   
 [IDiaAddressMap:: get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)   
 [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)
