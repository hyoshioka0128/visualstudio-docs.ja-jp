---
title: 'IDiaSession:: findSymbolsByRVAForAcceleratorPointerTag |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: a073cc45-0c7b-417e-b5fc-a3b08beccdbc
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0711c95310d4d3613d8b82bccbecab122bf19ef8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196360"
---
# <a name="idiasessionfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSession::findSymbolsByRVAForAcceleratorPointerTag
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このメソッドは、対応するタグ値を指定して、指定された相対仮想アドレスで、指定された親アクセラレータのスタブ関数に含まれるシンボルの列挙体を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findSymbolsByRVAForAcceleratorPointerTag (   
   IDiaSymbol*           parent,  
   DWORD                 tagValue,  
   DWORD                 rva,  
   IDiaEnumSymbols**     ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `parent`  
 から `IDiaSymbol` 検索するアクセラレータスタブ関数に対応する。  
  
 `tagValue`  
 からポインターのタグ値。  
  
 `rva`  
 から相対仮想アドレス。  
  
 `ppResult`  
 入出力結果を使用し `IDiaEnumSymbols` て初期化されるインターフェイスポインターへのポインター。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、 `IDiaSymbol` アクセラレータスタブ関数に対応するインターフェイスでのみ呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
