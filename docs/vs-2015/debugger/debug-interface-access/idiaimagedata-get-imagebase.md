---
title: 'IDiaImageData:: get_imageBase |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_imageBase method
ms.assetid: 4ba3d9e4-b205-4ee6-a41d-6996972f1f85
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a4a8ed3f52a6e4709aa9553b0d7cc906069c9bcd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202577"
---
# <a name="idiaimagedataget_imagebase"></a>IDiaImageData::get_imageBase
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

イメージの基になるメモリ位置を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_imageBase (   
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力推奨されるイメージのベース値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 イメージベースの競合により、イメージが読み込まれるときに、未使用のメモリ位置に自動的に再配置される場合があります。 このメソッドは、コンパイル時にモジュールに格納された基本ヒント (推奨されるメモリの場所) を返します。  
  
## <a name="see-also"></a>参照  
 [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)
