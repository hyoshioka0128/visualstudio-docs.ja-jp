---
title: IDiaAddressMap::put_imageAlign | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_imageAlign method
ms.assetid: f9ce875d-c263-43e5-a534-f34c37f9866f
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5e0fa57c38c8451bde84d96ab32bc7980c5e2d8b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841664"
---
# <a name="idiaaddressmapput_imagealign"></a>IDiaAddressMap::put_imageAlign
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

イメージの配置を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT put_imageAlign (   
   DWORD NewVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 NewVal  
 から実行可能ファイルの新しいイメージの配置値。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 イメージ (読み込まれた実行可能ファイル) は、指定されたメモリ境界に合わせて調整されます。 このアラインメントは、現在のシステムアーキテクチャと、コンパイルおよびリンク時のオプションによって影響を受ける可能性があります。 イメージの配置は、常にバイト境界上にあります。 次の画像の配置値は有効です: 1、2、4、8、16、32、および64バイト境界。  
  
 現在のイメージの配置は、 [IDiaAddressMap:: get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md) メソッドを呼び出すことによって取得できます。  
  
> [!NOTE]
> イメージは、このメソッドを呼び出すことができる時間によって既に読み込まれています。 通常、メソッドは、 `put_imageAlign` イメージが移動または変更され、新しい配置が必要なときに使用されます。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)
