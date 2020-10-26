---
title: 'IDiaPropertyStorage:: ReadBOOL |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBOOL
ms.assetid: ad1822db-4572-48f7-9919-f8137f6701f2
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 64eee421a5ed5bd46a64b51694d913a4f2dc4d41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538877"
---
# <a name="idiapropertystoragereadbool"></a>IDiaPropertyStorage::ReadBOOL
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

`BOOL`プロパティセット内の値を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT ReadBOOL (   
   PROPID id,  
   BOOL*  pValue  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 から読み取るプロパティの識別子 ( `PROPID` は WTypes .h でとして定義されてい `ULONG` ます)。  
  
 `pValue`  
 入出力プロパティ値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `E_INVALIDARG`プロパティが型でない場合は、を返し `BOOL` ます。  
  
## <a name="remarks"></a>注釈  
 一貫した結果を得るために、 `BOOL` 0 以外の値がで0がになるように値を解釈し `TRUE` `FALSE` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
