---
title: IDiaEnumLineNumbers |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers interface
ms.assetid: cdf07b4f-19e4-4dcd-8af8-c2dbca586a7c
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 87d5450cddab6b3cd230040175d18ae186483b30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687192"
---
# <a name="idiaenumlinenumbers"></a>IDiaEnumLineNumbers
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

データソースに格納されているさまざまな行番号を列挙します。  
  
## <a name="syntax"></a>構文  
  
```  
IDiaEnumLineNumbers : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDiaEnumLineNumbers` ます。  
  
|Method|説明|  
|------------|-----------------|  
|[IDiaEnumLineNumbers::get__NewEnum](../../debugger/debug-interface-access/idiaenumlinenumbers-get-newenum.md)|この列挙子の [IEnumVARIANT インターフェイス](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e) バージョンを取得します。|  
|[IDiaEnumLineNumbers::get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md)|行番号の数を取得します。|  
|[IDiaEnumLineNumbers::Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)|インデックスを使って行番号を取得します。|  
|[IDiaEnumLineNumbers::Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md)|列挙シーケンス内の指定された数の行番号を取得します。|  
|[IDiaEnumLineNumbers::Skip](../../debugger/debug-interface-access/idiaenumlinenumbers-skip.md)|列挙シーケンス内の指定された数の行番号をスキップします。|  
|[IDiaEnumLineNumbers::Reset](../../debugger/debug-interface-access/idiaenumlinenumbers-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[IDiaEnumLineNumbers::Clone](../../debugger/debug-interface-access/idiaenumlinenumbers-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
  
## <a name="remarks"></a>解説  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスは、 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) インターフェイスで次のいずれかのメソッドを呼び出すことによって取得されます。  
  
- [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)  
  
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)  
  
- [IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)  
  
- [IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)  
  
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)  
  
## <a name="example"></a>例  
 この例では、セッションからインターフェイスを取得する方法を示し `IDiaEnumLineNumbers` ます。 この例では、関数の行番号の列挙を取得する方法を示しています (で表さ `pSymbol` れます)。 行番号を使用する詳細な例については、 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) インターフェイスを参照してください。  
  
```cpp#  
void dumpFunctionLines( IDiaSymbol* pSymbol, IDiaSession* pSession )  
{  
    ULONGLONG length = 0;  
    DWORD isect = 0;  
    DWORD offset = 0;  
    pSymbol->get_addressSection( &isect );  
    pSymbol->get_addressOffset( &offset );  
    pSymbol->get_length( &length );  
    if ( isect != 0 && length > 0 )  
    {  
        CComPtr< IDiaEnumLineNumbers > pLines;  
        if ( SUCCEEDED( pSession->findLinesByAddr(  
                                      isect,  
                                      offset,  
                                      static_cast<DWORD>( length ),  
                                      &pLines )  
                      )  
           )  
        {  
            // Do something with the enumeration  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSession:: findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)   
 [IDiaSession:: Find Byrva](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)   
 [IDiaSession:: Find Byva](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)   
 [IDiaSession:: findLines](../../debugger/debug-interface-access/idiasession-findlines.md)   
 [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)
