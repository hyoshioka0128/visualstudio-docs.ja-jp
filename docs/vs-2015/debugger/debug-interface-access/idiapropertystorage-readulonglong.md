---
title: 'IDiaPropertyStorage:: ReadULONGLONG |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadULONGLONG
ms.assetid: f80a2e24-5744-4fec-bab0-3ed51aef6e58
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6da509e226a612e80a10ca0759b5e264f31a1e13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538682"
---
# <a name="idiapropertystoragereadulonglong"></a>IDiaPropertyStorage::ReadULONGLONG
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

`ULONGLONG`プロパティセット内の値を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT ReadULONGLONG (   
   PROPID     id,  
   ULONGLONG* pValue  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 から読み取るプロパティの識別子 ( `PROPID` は WTypes .h でとして定義されてい `ULONG` ます)。  
  
 `pValue`  
 入出力プロパティ値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `E_INVALIDARG`プロパティが型でない場合は、を返し `ULONGLONG` ます。  
  
## <a name="remarks"></a>注釈  
 は、 `ULONGLONG` Windows によって64ビット符号なし整数として定義されます。  
  
## <a name="see-also"></a>参照  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
