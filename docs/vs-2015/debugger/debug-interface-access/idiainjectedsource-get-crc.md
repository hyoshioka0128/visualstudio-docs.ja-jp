---
title: 'IDiaInjectedSource:: get_crc |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_crc method
ms.assetid: 2ecdda93-950e-40d6-b79b-4ae3c55b6cfc
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fb62e5ad1d67f0e7bc85692935e64f85eb1c72df
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202206"
---
# <a name="idiainjectedsourceget_crc"></a>IDiaInjectedSource::get_crc
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソースコードのバイトから計算された巡回冗長検査 (CRC) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_crc (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力ソースコードのバイトから計算された CRC を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`このプロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
