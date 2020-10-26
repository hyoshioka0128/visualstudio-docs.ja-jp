---
title: 'IDiaStackFrame:: get_lengthLocals |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_lengthLocals method
ms.assetid: dbc3e544-578a-4f0b-8d20-f21ad4cbb604
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 364783f2287c363b82cf84bdc0e441e82307598e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190553"
---
# <a name="idiastackframeget_lengthlocals"></a>IDiaStackFrame::get_lengthLocals
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

スタックにプッシュされたローカル変数のバイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_lengthLocals (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力ローカル変数のバイト数を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`プロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
