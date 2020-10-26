---
title: IDiaReadExeAtRVACallback::ReadExecutableAtRVA | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback::ReadExecutableAtRVA method
ms.assetid: 3c1e965f-8f05-41a8-86d8-01830b2377c9
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8d74543b7b57d188712c04bc43429357a5140c9e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187274"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

実行可能ファイルから、指定された相対仮想アドレス (RVA) を開始位置として、指定されたバイト数を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT ReadExecutableAtRVA (   
   DWORD  relativeVirtualAddress,  
   DWORD  cbData,  
   DWORD* pcbData,  
   BYTE   data[]  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `relativeVirtualAddress`  
 から読み取りを開始する実行可能ファイル内の RVA。  
  
 `cbData`  
 から読み取るバイト数。  
  
 `pcbData`  
 入出力読み取ったバイト数を返します。  
  
 `data[]`  
 [入力、出力]ファイルから読み取ったバイトを格納する配列。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、DIA サポートコードによって呼び出され、相対仮想アドレスを使用して実行可能ファイルからデータバイトを読み込みます。 このメソッドは、 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドをサポートするために呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)   
 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
