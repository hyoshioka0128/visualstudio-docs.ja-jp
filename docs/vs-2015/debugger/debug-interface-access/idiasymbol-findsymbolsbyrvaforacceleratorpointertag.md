---
title: 'IDiaSymbol:: findSymbolsByRVAForAcceleratorPointerTag |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 024ccd78-5867-4ca7-bc26-548758e9ac53
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ee1aea023124fb8277fd13cf341a63fca92c37cd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149867"
---
# <a name="idiasymbolfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

対応するタグ値が指定されている場合、このメソッドは、指定された相対仮想アドレスで、このスタブ関数に含まれるシンボルの列挙体を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT findSymbolsByRVAForAcceleratorPointerTag (   
   DWORD             tagValue,  
   DWORD             rva,  
   IDiaEnumSymbols** ppResult);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `tagValue`  
 からPointee シンボルレコードが存在するポインタータグ値。  
  
 `rva`  
 から指定されたタグ値を持つ pointee 変数に対応するシンボルをフィルター処理するために使用される rva。  
  
 `ppResult`  
 入出力結果を使用し `IDiaEnumSymbols` て初期化されるインターフェイスポインターへのポインター。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、 `IDiaSymbol` アクセラレータスタブ関数に対応するインターフェイスでのみ呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
