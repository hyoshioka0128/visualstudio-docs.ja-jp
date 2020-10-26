---
title: IDiaTable |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5b9c9f85ffbf4eed2fdc305a64bd3f32822dacd6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682786"
---
# <a name="idiatable"></a>IDiaTable
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

DIA データソーステーブルを列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaTable : IEnumUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDiaTable` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|この列挙子の [IEnumVARIANT インターフェイス](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e) バージョンを取得します。|  
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|テーブルの名前を取得します。|  
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|テーブル内の項目の数を取得します。|  
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|特定のエントリインデックスへの参照を取得します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは `IEnumUnknown` 、VisualStudio 名前空間で列挙メソッドを実装します。 `IEnumUnknown`列挙インターフェイスは、 [IDiaTable:: get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)メソッドと[IDiaTable:: Item](../../debugger/debug-interface-access/idiatable-item.md)メソッドよりもテーブルの内容を反復処理する場合に、はるかに効率的です。  
  
 `IUnknown` `IDiaTable::Item` メソッドまたはメソッド (VisualStudio 名前空間内) のいずれかから返されるインターフェイスの解釈 `Next` は、テーブルの種類によって異なります。 たとえば、 `IDiaTable` インターフェイスが挿入されたソースのリストを表す場合は、 `IUnknown` [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) インターフェイスに対してインターフェイスに対してクエリを行う必要があります。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスを取得するには、 [IDiaEnumTables:: Item](../../debugger/debug-interface-access/idiaenumtables-item.md) または [IDiaEnumTables:: Next](../../debugger/debug-interface-access/idiaenumtables-next.md) メソッドを呼び出します。  
  
 インターフェイスでは、次のインターフェイスが実装され `IDiaTable` ます (つまり、次のいずれかのインターフェイスに対してインターフェイスに対してクエリを実行でき `IDiaTable` ます)。  
  
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)  
  
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)  
  
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)  
  
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)  
  
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)  
  
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)  
  
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)  
  
## <a name="example"></a>例  
 1つ目の関数は、 `ShowTableNames` セッション内のすべてのテーブルの名前を表示します。 2番目の関数は、すべてのテーブルで、 `GetTable` 指定したインターフェイスを実装するテーブルを検索します。 3番目の関数は、 `UseTable` 関数の使用方法を示して `GetTable` います。  
  
> [!NOTE]
> `CDiaBSTR` は、をラップし、 `BSTR` インスタンス化がスコープ外になったときに文字列の解放を自動的に処理するクラスです。  
  
```cpp#  
void ShowTableNames(IDiaSession *pSession)  
{  
    CComPtr<IDiaEnumTables> pTables;  
    if ( FAILED( psession->getEnumTables( &pTables ) ) )  
    {  
        Fatal( "getEnumTables" );  
    }  
    CComPtr< IDiaTable > pTable;  
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) )  
            && celt == 1 )  
    {  
        CDiaBSTR bstrTableName;  
        if ( pTable->get_name( &bstrTableName ) != 0 )  
        {  
            Fatal( "get_name" );  
        }  
        printf( "Found table: %ws\n", bstrTableName );  
    }  
  
// Searches the list of all tables for a table that supports  
// the specified interface.  Use this function to obtain an  
// enumeration interface.  
HRESULT GetTable(IDiaSession* pSession,  
                 REFIID       iid,  
                 void**       ppUnk)  
{  
    CComPtr<IDiaEnumTables> pEnumTables;  
    HRESULT hResult;  
  
    if (FAILED(pSession->getEnumTables(&pEnumTables)))  
        Fatal("getEnumTables");  
  
    CComPtr<IDiaTable> pTable;  
    ULONG celt = 0;  
    while (SUCCEEDED(hResult = pEnumTables->Next(1, &pTable, &celt)) &&  
           celt == 1)  
    {  
        if (pTable->QueryInterface(iid, (void**)ppUnk) == S_OK)  
        {  
            return S_OK;  
        }  
        pTable = NULL;  
    }  
  
    if (FAILED(hResult))  
        Fatal("EnumTables->Next");  
  
    return E_FAIL;  
}  
  
// This function shows how to use the GetTable function.  
void UseTable(IDiaSession *pSession)  
{  
    CComPtr<IDiaEnumSegments> pEnumSegments;  
    if (SUCCEEDED(GetTable(pSession, __uuidof(IDiaEnumSegments), &pEnumSegments)))  
    {  
        // Do something with pEnumSegments.  
    }  
}  
```  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)   
 [IDiaEnumTables:: Item](../../debugger/debug-interface-access/idiaenumtables-item.md)   
 [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
