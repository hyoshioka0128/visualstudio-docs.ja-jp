---
title: 'IDiaPropertyStorage:: ReadPropertyNames |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadPropertyNames
ms.assetid: f8bcab77-afca-4a8f-8710-697842f8a518
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f3f6d3ac520a396b5207767a3fec0913c801c287
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62537421"
---
# <a name="idiapropertystoragereadpropertynames"></a>IDiaPropertyStorage::ReadPropertyNames
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定されたプロパティ識別子の対応する文字列名を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ReadPropertyNames (  
   ULONG         cpropid,  
   PROPID const* rgpropid,  
   BSTR*         rglpwstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cpropid`  
 からのプロパティ id の数 `rgpropid` 。  
  
 `rgpropid`  
 から名前を取得する対象のプロパティ id の配列 ( `PROPID` は、WTypes .h でとして定義されてい `ULONG` ます)。  
  
 `rglpwstrName`  
 [入力、出力]指定されたプロパティ id のプロパティ名の配列。 配列は、要求された数のプロパティ名を保持するために事前に割り当てられている必要があり、少なくとも文字列を保持できる必要があり `cpropid``BSTR` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 返されたプロパティ名は、不要になったときに (関数を呼び出すことによって) 解放する必要があり `SysFreeString` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
