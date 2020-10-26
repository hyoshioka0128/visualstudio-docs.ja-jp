---
title: 'IDiaFrameData:: get_type |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_type method
ms.assetid: efca38b5-c479-4d0a-a164-f903f25c5509
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 95232ab69d6f30435807764e1177d15d6e4622d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161434"
---
# <a name="idiaframedataget_type"></a>IDiaFrameData::get_type
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コンパイラ固有のフレームの種類を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_type (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力コンパイラ固有のフレームの種類を示す、 [stackframe Typeenum](../../debugger/debug-interface-access/stackframetypeenum.md) 列挙型の値を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`このプロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [StackFrameTypeEnum 列挙型](../../debugger/debug-interface-access/stackframetypeenum.md)
