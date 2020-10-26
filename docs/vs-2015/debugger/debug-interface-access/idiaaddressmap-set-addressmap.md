---
title: IDiaAddressMap::set_addressMap | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 693ecf6e8fd4f0b55936bde371b7baa6975b8f2c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198655"
---
# <a name="idiaaddressmapset_addressmap"></a>IDiaAddressMap::set_addressMap
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

画像レイアウトの翻訳をサポートするアドレスマップを提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT set_addressMap (   
   DWORD                     cbData,  
   struct DiaAddressMapEntry data[],  
   BOOL                      imagetoSymbols  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cbData`  
 からパラメーター内の要素の数 `data` 。  
  
 `data[]`  
 から変換マップを定義する [DiaAddressMapEntry 構造](../../debugger/debug-interface-access/diaaddressmapentry.md) 体の配列。  
  
 `imagetoSymbols`  
 [入力] `TRUE` パラメーターで、 `data` 新しいイメージレイアウトから元のレイアウトへのマップを定義する場合は (デバッグシンボルの説明を参照)。 `FALSE``data`が元のレイアウトから取得された新しいイメージレイアウトへのマップである場合は。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 通常、DIA は、プログラムデータベース (.pdb) ファイルからアドレス変換マップを取得します。 これらの値が欠落している場合は、 [IDiaAddressMap:: set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) メソッドが2回呼び出されます。1回は、 `imagetoSymbols` パラメーターをに設定し、パラメーターを `TRUE` `imagetoSymbols` に設定し `FALSE` ます。 両方の変換マップが指定されていない限り、 [IDiaAddressMap::p ut_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md) メソッドを使用してアドレスマップの翻訳を有効にすることはできません。  
  
## <a name="see-also"></a>参照  
 [DiaAddressMapEntry 構造体](../../debugger/debug-interface-access/diaaddressmapentry.md)   
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::p ut_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
