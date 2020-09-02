---
title: 'IDiaAddressMap:: get_addressMapEnabled |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_addressMapEnabled method
ms.assetid: 6183dc5e-befa-4e5a-ae5a-f4aa24f3ed9e
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0cf874590d6bcf7f259d7a59eee1b81b79ffe1a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178242"
---
# <a name="idiaaddressmapget_addressmapenabled"></a>IDiaAddressMap::get_addressMapEnabled
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

特定のセッションに対してアドレスマップが確立されているかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_addressMapEnabled (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 の場合は、  
 入出力 `TRUE` アドレスマッピングが有効になっている場合はを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 実行可能なプロセッサの後で、実行可能ファイルが更新されることがあります。 DIA には、新しいレイアウトへのシンボルの変換をサポートする機構が含まれています。  
  
 クライアントアプリケーションは、 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)インターフェイスから[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)インターフェイスを取得し、 [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)メソッドを呼び出した後、 [IDiaAddressMap::p ut_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)メソッドを呼び出すことによって、特定のセッションのアドレスマップを設定できます。 メソッドは、 `get_addressMapEnabled` メソッドを呼び出した結果を返し `put_addressMapEnabled` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)   
 [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
