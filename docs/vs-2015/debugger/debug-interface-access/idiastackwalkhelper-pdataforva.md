---
title: IDiaStackWalkHelper::p dataForVA |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::pdataByVA method
ms.assetid: fafc38fe-74dc-4726-9a51-eebf3a673d7f
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5af921caa989d7279bb9f52751c452d91045cf3e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150084"
---
# <a name="idiastackwalkhelperpdataforva"></a>IDiaStackWalkHelper::pdataForVA
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

仮想アドレスに関連付けられている PDATA データブロックを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT pdataForVA(   
   ULONGLONG  va,  
   DWORD      cbData,  
   DWORD*     pcbData,  
   BYTE*      pbData  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `va`  
 から取得するデータの仮想アドレスを指定します。  
  
 `cbData`  
 から取得するデータのサイズ (バイト単位)。  
  
 `pcbData`  
 入出力取得したデータの実際のサイズをバイト単位で返します。  
  
 `pbData`  
 [入力、出力]要求されたデータを格納するバッファー。 `NULL` にすることはできません。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`指定されたアドレスに PDATA がない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 コンパイル単位の PDATA ("pdata" という名前のセクション) には、関数の例外処理に関する情報が含まれています。  
  
 呼び出し元は、返されるデータの量を認識しているため、呼び出し元は使用できるデータの量を確認する必要がありません。 このため、パラメーターがの場合、このメソッドの実装でエラーが返されることは許容され `pbData` `NULL` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
