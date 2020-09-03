---
title: IDiaAddressMap::put_relativeVirtualAddressEnabled | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_relativeVirtualAddressEnabled method
ms.assetid: 767c078e-8ad7-4940-9e00-cae7704aadee
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 14c9924346471e098d9ba9f1abb52fda0d3c9969
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198671"
---
# <a name="idiaaddressmapput_relativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

クライアントが相対仮想アドレス (RVA) の計算と使用を有効または無効にすることを許可します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT put_relativeVirtualAddressEnabled (   
   BOOL NewVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 NewVal  
 からをに設定すると `TRUE` 、が有効に `FALSE` なり、無効になります。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 DIA インターフェイスによって記述され、実行可能ファイルのイメージベースに対して相対的なデバッグオブジェクトのアドレスは、相対仮想アドレスとして取得できます。  
  
 RVAs の使用は、セグメントが PDB ファイルから最初に読み込まれるときに有効になります。 RVAs の使用の現在の状態を取得するには、 [IDiaAddressMap:: get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) メソッドを呼び出します。  
  
 `put_relativeVirtualAddress` [IDiaAddressMap:: set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)メソッドへの正常な呼び出しによって新しいイメージヘッダーが確立された後に、メソッドを呼び出して RVAs を有効にする必要があります。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap:: get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
