---
title: 'IDiaStackFrame:: get_rawLVarInstanceValue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_rawLVarInstanceValue method
ms.assetid: ce526259-85a6-475b-9274-0b3a21d95db2
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8ff78c38ad077084b3dea9c96e3251ffddb2206
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62573015"
---
# <a name="idiastackframeget_rawlvarinstancevalue"></a>IDiaStackFrame::get_rawLVarInstanceValue
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このメソッドは、指定されたローカル変数の値を生のバイトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_rawLVarInstanceValue(  
   IDiaLVarInstance* pInstance,  
   DWORD             cbDataMax,  
   DWORD*            pcbData,  
   BYTE*             pbData  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pInstance`  
 から `IDiaLVarInstance` 値を取得するローカル変数のインスタンスを表すオブジェクト。  
  
 `cbDataMax`  
 からが指すバッファー内の最大バイト数 `pbData` 。 最大8バイト () にすることができ `sizeof(ULONGLONG)` ます。  
  
 `pcbData`  
 入出力バッファーに格納されている実際のバイト数を返します。  
  
 `pbData`  
 入出力データを格納するバッファー。 これは `NULL` にすることはできません。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
