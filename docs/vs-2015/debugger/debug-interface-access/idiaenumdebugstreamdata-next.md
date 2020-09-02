---
title: 'IDiaEnumDebugStreamData:: Next |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Next method
ms.assetid: 114171dd-38fd-4bd7-a702-8ff887ffc99b
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4bdbf58321426890bffd45a08818dc5341bdfc3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187394"
---
# <a name="idiaenumdebugstreamdatanext"></a>IDiaEnumDebugStreamData::Next
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列挙されたシーケンス内の指定した数のレコードを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Next (   
   ULONG  celt,  
   DWORD  cbData,  
   DWORD* pcbData,  
   BYTE   data[],  
   ULONG* pceltFetched  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 celt  
 から取得するレコードの数。  
  
 cbData  
 からデータバッファーのサイズ (バイト単位)。  
  
 pcbData  
 入出力返されたバイト数を返します。 `data`が NULL の場合、には、 `pcbData` 要求されたすべてのレコードで使用可能なデータの合計バイト数が格納されます。  
  
 data[]  
 入出力デバッグストリームレコードデータを格納するバッファー。  
  
 pceltFetched  
 [入力、出力]内のレコードの数を返し `data` ます。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`それ以上レコードがない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)   
 [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)
