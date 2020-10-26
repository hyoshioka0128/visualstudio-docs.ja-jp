---
title: 'IDiaPropertyStorage:: ReadBSTR |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBSTR
ms.assetid: 7214643b-3286-48ed-90aa-0fe95b4cae5b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e0c7a796a57d5c96d870850bb02051d745fd8473
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538830"
---
# <a name="idiapropertystoragereadbstr"></a>IDiaPropertyStorage::ReadBSTR
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

`BSTR`プロパティセット内の値を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT ReadBSTR (   
   PROPID id,  
   BSTR*  pValue  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 から読み取るプロパティの識別子 ( `PROPID` は WTypes .h でとして定義されてい `ULONG` ます)。  
  
 `pValue`  
 入出力プロパティ値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `E_INVALIDARG`プロパティが型でない場合は、を返し `BSTR` ます。  
  
## <a name="remarks"></a>注釈  
 は、 `BSTR` Windows によって、0で終わるワイド文字列として定義されます。  
  
## <a name="see-also"></a>参照  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
