---
title: Idiaaddressmap::put_relativevirtualaddressenabled |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_relativeVirtualAddressEnabled method
ms.assetid: 767c078e-8ad7-4940-9e00-cae7704aadee
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d0b9e908e03dced75bf8fa3dfce3f31e6bbe148b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49827365"
---
# <a name="idiaaddressmapputrelativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
クライアントは有効または、計算と相対仮想アドレス (RVA) の使用を無効にできます。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT put_relativeVirtualAddressEnabled (   
   BOOL NewVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 NewVal  
 [in]設定`TRUE`を有効にする、または`FALSE`を無効にします。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 DIA インターフェイス、および実行可能ファイルのイメージのベースを基準と説明されているデバッグ オブジェクトのアドレスは、相対仮想アドレスとして取得できます。  
  
 セグメントが PDB ファイルから最初に読み込まれるときに、Rva の使用を有効になっています。 Rva の使用の現在の状態を取得する、 [idiaaddressmap::get_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)メソッド。  
  
 `put_relativeVirtualAddress`に成功した呼び出しの後の Rva を有効にするメソッドを呼び出す必要があります、 [idiaaddressmap::set_imageheaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)メソッドが新しいイメージのヘッダーを確立します。  
  
## <a name="see-also"></a>関連項目  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [Idiaaddressmap::get_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)