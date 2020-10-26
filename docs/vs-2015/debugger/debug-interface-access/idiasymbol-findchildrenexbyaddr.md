---
title: 'IDiaSymbol:: findChildrenExByAddr |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenExByAddr
ms.assetid: c1e7885d-2d15-4529-9ac2-32dd22efe31c
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8f791074d029be78eb7d45e06dce8a8cce145f71
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149999"
---
# <a name="idiasymbolfindchildrenexbyaddr"></a>IDiaSymbol::findChildrenExByAddr
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定されたアドレスで有効なシンボルの子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findChildrenExByAddr (   
   enum SymTagEnum   symtag,  
   LPCOLESTR         name,  
   DWORD             compareFlags,  
   DWORD             address,  
   IDiaEnumSymbols** ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `symtag`  
 から [Symtagenum 列挙体](../../debugger/debug-interface-access/symtagenum.md)で定義されている、取得する子のシンボルタグを指定します。 すべての子を取得するには、をに設定 `SymTagNull` します。  
  
 `name`  
 から取得する子の名前を指定します。 すべての子を取得するには、をに設定 `NULL` します。  
  
 `compareFlags`  
 から名前の一致に適用する比較オプションを指定します。 [Namesearchoptions 列挙](../../debugger/debug-interface-access/namesearchoptions.md)列挙の値は、単独で、または組み合わせて使用できます。  
  
 `address`  
 から記号のアドレス。  
  
 `ppResult`  
 入出力取得した子シンボルのリストを格納している [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`シンボルの少なくとも1つの子が見つかった場合はを返し、子が見つからなかった場合はを返し `S_FALSE` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 返されるローカルシンボルには、live range 情報が含まれます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia100.dll  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSession:: findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)
