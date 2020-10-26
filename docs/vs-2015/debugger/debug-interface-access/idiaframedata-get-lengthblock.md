---
title: 'IDiaFrameData:: get_lengthBlock |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthBlock method
ms.assetid: 2e54deb7-7744-428e-913c-1d47a2aa89b0
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7d66e8cd69836a6c2f8ee1052f5f5f7ff789f736
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62552541"
---
# <a name="idiaframedataget_lengthblock"></a>IDiaFrameData::get_lengthBlock
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

フレームによって記述されたコードブロックの長さをバイト単位で取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_lengthBlock (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力フレーム内のコードのバイト数を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`このプロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドによって返される値は、通常、プログラム文字列の解釈に使用されます (プログラム文字列の定義については、 [IDiaFrameData:: get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) メソッドを参照してください)。  
  
## <a name="see-also"></a>参照  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
