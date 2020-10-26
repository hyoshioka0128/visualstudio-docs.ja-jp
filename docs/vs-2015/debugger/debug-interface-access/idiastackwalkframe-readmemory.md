---
title: 'IDiaStackWalkFrame:: readMemory |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::readMemory method
ms.assetid: 7ab0b525-a5a7-4692-acad-e8c00fa9ab9a
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 97a868973d2a514150b8d728e685523e918f88f4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150161"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

イメージからメモリを読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT readMemory (   
   MemoryTypeEnum type,  
   ULONGLONG va,  
   DWORD     cbData,  
   DWORD*    pcbData,  
   BYTE      data[]  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `type`  
 からアクセスするメモリの種類を指定する [Memorytypeenum 列挙](../../debugger/debug-interface-access/memorytypeenum.md) 値の1つ。  
  
 `va`  
 から読み取りを開始するイメージ内の仮想アドレスの場所。  
  
 `cbData`  
 からデータバッファーのサイズ (バイト単位)。  
  
 `pcbData`  
 入出力返されたバイト数を返します。 がの場合 `data` `NULL` 、には、 `pcbData` 使用可能なデータの合計バイト数が含まれます。  
  
 `data`  
 入出力指定された場所からデータを格納するバッファー。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
