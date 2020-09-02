---
title: 'IDiaStackFrame:: get_type |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_type method
ms.assetid: 99daa97b-5c05-455d-bd1e-800762ccf7c9
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b4b0653de51ece59584076def76988958ae612d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68144741"
---
# <a name="idiastackframeget_type"></a>IDiaStackFrame::get_type
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

フレームの種類を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_type (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力 [Stackフレーム Typeenum](../../debugger/debug-interface-access/stackframetypeenum.md) 列挙型の列挙体から値を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`プロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)   
 [StackFrameTypeEnum 列挙型](../../debugger/debug-interface-access/stackframetypeenum.md)
