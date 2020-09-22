---
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 580637cf1058c8bfbd10ac7812e59c802830d95e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841976"
---
# <a name="idiasymbolget_registerid"></a>IDiaSymbol::get_registerId
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[LocationType 列挙](../../debugger/debug-interface-access/locationtype.md)がに設定されている場合の、場所のレジスタ指定子を取得し `LocIsEnregistered` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_registerId (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力場所のレジスタ指定子を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 シンボルがレジスタに対して相対的な場合、つまり、シンボルの [LocationType 列挙](../../debugger/debug-interface-access/locationtype.md) がに設定されている場合は、メソッドを使用し、 `LocIsRegRel` `get_registerId` その後に [IDiaSymbol:: get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md) メソッドを呼び出して、シンボルが配置されているレジスタからのオフセットを取得します。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
