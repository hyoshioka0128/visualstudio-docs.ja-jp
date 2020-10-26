---
title: 'IDiaStackFrame:: get_registerValue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_registerValue method
ms.assetid: cbe3d8ac-319a-40ac-bc3e-4eb81b2d7807
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3b8038acf2aef8c34d07e7f21543a597ad7b96fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62572986"
---
# <a name="idiastackframeget_registervalue"></a>IDiaStackFrame::get_registerValue
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

スタックフレームに格納されている、指定したレジスタの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_registerValue(  
   ULONG      registerIndex,  
   ULONGLONG *pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `registerIndex`  
 から [CV_HREG_e 列挙](../../debugger/debug-interface-access/cv-hreg-e.md) 型の列挙値の1つ。  
  
 `pRetVal`  
 入出力レジスタに格納されている値。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)   
 [CV_HREG_e 列挙型](../../debugger/debug-interface-access/cv-hreg-e.md)
