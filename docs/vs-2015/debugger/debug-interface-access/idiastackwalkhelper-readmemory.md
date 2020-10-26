---
title: 'IDiaStackWalkHelper:: readMemory |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8bef01cd29bb2312bd682f2f1f1150ee78da293e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150067"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

メモリ内の実行可能イメージからデータブロックを読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT readMemory(   
   enum MemoryTypeEnum type,  
   ULONGLONG           va,  
   DWORD               cbData,  
   DWORD*              pcbData,  
   BYTE*               pbData  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `type`  
 から読み取るメモリの型を指定する [Memorytypeenum](../../debugger/debug-interface-access/memorytypeenum.md) 列挙型の値。  
  
 va  
 から読み取りを開始するイメージの仮想アドレス。  
  
 `cbData`  
 からデータバッファーのサイズ (バイト単位)。  
  
 `pcbData`  
 入出力実際に読み取られたバイト数を返します。 がの場合は `pbData` `NULL` 、使用可能なデータの合計バイト数です。  
  
 `pbData`  
 [入力、出力]読み取られたメモリに格納されているバッファー。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)   
 [MemoryTypeEnum 列挙型](../../debugger/debug-interface-access/memorytypeenum.md)
