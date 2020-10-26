---
title: IDiaAddressMap::get_relativeVirtualAddressEnabled | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_relativeVirtualAddressEnabled method
ms.assetid: 4c48af81-7148-4d9a-818e-dbe62cbfc638
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fc04b50e718720ee13997b32cc7b102e8d96d0bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198697"
---
# <a name="idiaaddressmapget_relativevirtualaddressenabled"></a>IDiaAddressMap::get_relativeVirtualAddressEnabled
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

計算と相対仮想アドレス (RVA) の使用が有効かどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_relativeVirtualAddressEnabled (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 の場合は、  
 入出力 `TRUE` RVAs の計算が有効になっている場合は、を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 RVAs は、セグメントが PDB ファイルから最初に読み込まれた場合に有効になります。 [IDiaAddressMap::p ut_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)メソッドを呼び出すことによって、RVAs の使用を一時的に無効にすることができます。  
  
 また、新しいイメージヘッダーを設定するには、 [IDiaAddressMap:: set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) メソッドを呼び出した後、メソッドを呼び出して、 `put_relativeVirtualAddressEnabled` 新しいイメージヘッダーを使用して RVAs を使用できるようにします。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap:: set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)   
 [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)
