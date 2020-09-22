---
title: IDiaEnumSymbols |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols interface
ms.assetid: 649f7bfd-86ac-49a5-8533-aff77e1bc62e
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fae39270cfbbbb93b106de65b3b01210ffc61d29
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841557"
---
# <a name="idiaenumsymbols"></a>IDiaEnumSymbols
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

データソースに格納されているさまざまなシンボルを列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaEnumSymbols : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDiaEnumSymbols` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaEnumSymbols::get__NewEnum](../../debugger/debug-interface-access/idiaenumsymbols-get-newenum.md)|`IEnumVARIANT Interface`この列挙子のバージョンを取得します。|  
|[IDiaEnumSymbols::get_Count](../../debugger/debug-interface-access/idiaenumsymbols-get-count.md)|シンボルの数を取得します。|  
|[IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)|インデックスを使ってシンボルを取得します。|  
|[IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)|列挙シーケンス内の指定された数のシンボルを取得します。|  
|[IDiaEnumSymbols::Skip](../../debugger/debug-interface-access/idiaenumsymbols-skip.md)|列挙シーケンス内の指定された数のシンボルをスキップします。|  
|[IDiaEnumSymbols::Reset](../../debugger/debug-interface-access/idiaenumsymbols-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[IDiaEnumSymbols::Clone](../../debugger/debug-interface-access/idiaenumsymbols-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、 `SymTagUDT` (ユーザー定義型) やなど、特定の種類のシンボルによってグループ化されたシンボルを提供 `SymTagBaseClass` します。 アドレスによってグループ化されたシンボルを操作するには、 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md) インターフェイスを使用します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスを取得するには、次のメソッドを呼び出します。  
  
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)  
  
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)  
  
- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)  
  
## <a name="example"></a>例  
 この例では、インターフェイスを取得 `IDiaEnumSymbols` し、その列挙体を使用してユーザー定義型 (udt) を一覧表示する方法を示します。  
  
> [!NOTE]
> `CDiaBSTR` は、をラップし、 `BSTR` インスタンス化がスコープ外になったときに文字列の解放を自動的に処理するクラスです。  
  
```cpp#  
void ShowUDTs(IDiaSymbol *pGlobals)  
{  
    CComPtr<IDiaEnumSymbols> pEnum;  
    CComPtr<IDiaSymbol> pSymbol;  
    HRESULT hr;  
  
    hr = pGlobals->findChildren(SymTagUDT,  
                                NULL,  
                                nsfCaseInsensitive | nsfUndecoratedName,  
                                &pEnum);  
    if (hr == S_OK)  
    {  
        while ( SUCCEEDED( hr = pEnum->Next( 1, &pSymbol, &celt ) ) &&  
                celt == 1 )  
        {  
            CDiaBSTR name;  
            if ( pSymbol->get_name( &name ) != S_OK )  
                Fatal( "get_name" );  
            printf( "Found UDT: %ws\n", name );  
            pSymbol = 0;  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession:: findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [IDiaSourceFile:: get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)   
 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
