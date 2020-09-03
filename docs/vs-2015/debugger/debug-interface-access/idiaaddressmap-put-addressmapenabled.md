---
title: IDiaAddressMap::put_addressMapEnabled | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4f2f7fc6fd512fa121cf96cb64f4ce4b961772e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198683"
---
# <a name="idiaaddressmapput_addressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

アドレスマップを使用してシンボルアドレスを変換する必要があるかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT put_addressMapEnabled (   
   BOOL NewVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 NewVal  
 から `TRUE` シンボルの変換を有効にする場合はに設定し、無効にする場合はに設定し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 実行可能なプロセッサの後で、実行可能ファイルが更新されることがあります。 DIA には、新しいレイアウトへのシンボルの変換をサポートする機構が含まれています。  
  
 PDB ファイルが読み込まれると、ファイルに格納されているアドレスマップが有効になります。 ただし、クライアントアプリケーションで [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) メソッドを呼び出すことによって独自のアドレスマップを指定することが必要になる場合があります。 `set_addressMap`メソッドが成功した場合、クライアントアプリケーションは、 `put_addressMapEnabled` のパラメーターを指定してメソッドを呼び出し、 `NewVal` `TRUE` そのアドレスマップを使用できるようにする必要があります。  
  
 有効になっているアドレスマップの現在の状態は、 [IDiaAddressMap:: get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md) メソッドを呼び出すことによって取得できます。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)   
 [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)
