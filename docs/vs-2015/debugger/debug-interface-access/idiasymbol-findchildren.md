---
title: 'IDiaSymbol:: findChildren |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildren method
ms.assetid: 5fe7573a-e48b-428d-9c17-7421b7209246
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a09a62a2e6b94dbccda3afce4bdd286270149c15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150037"
---
# <a name="idiasymbolfindchildren"></a>IDiaSymbol::findChildren
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

記号の子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findChildren (   
   enum SymTagEnum   symtag,  
   LPCOLESTR         name,  
   DWORD             compareFlags,  
   IDiaEnumSymbols** ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `symtag`  
 から [Symtagenum 列挙体](../../debugger/debug-interface-access/symtagenum.md)で定義されている、取得する子のシンボルタグを指定します。 すべての子を取得するには、をに設定 `SymTagNull` します。  
  
 `name`  
 から取得する子の名前を指定します。 すべての子を取得するには、をに設定 `NULL` します。  
  
 `compareFlags`  
 から名前の一致に適用される比較オプションを指定します。 [Namesearchoptions 列挙](../../debugger/debug-interface-access/namesearchoptions.md)列挙の値は、単独で、または組み合わせて使用できます。  
  
 `ppResult`  
 入出力取得した子シンボルのリストを格納している [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`シンボルの少なくとも1つの子が見つかった場合はを返し、子が見つからなかった場合はを返します。それ以外の場合は `S_FALSE` エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、このシンボルを最初のパラメーターとして [IDiaSession:: findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md) メソッドを呼び出すことと同じです。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSession:: findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)
