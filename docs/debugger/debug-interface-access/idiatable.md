---
title: IDiaTable |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bc7a573eb92d7c51079b0a7e97067abd155ae4fa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738707"
---
# <a name="idiatable"></a>IDiaTable
DIA データソーステーブルを列挙します。

## <a name="syntax"></a>構文

```
IDiaTable : IEnumUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表は、`IDiaTable` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|この列挙子の[IEnumVARIANT インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)バージョンを取得します。|
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|テーブルの名前を取得します。|
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|テーブル内の項目の数を取得します。|
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|特定のエントリインデックスへの参照を取得します。|

## <a name="remarks"></a>Remarks
このインターフェイスは、VisualStudio 名前空間の `IEnumUnknown` 列挙メソッドを実装します。 @No__t_0 列挙インターフェイスでは、 [IDiaTable:: get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)メソッドと[IDiaTable:: Item](../../debugger/debug-interface-access/idiatable-item.md)メソッドよりもテーブルの内容を反復処理する方がはるかに効率的です。

@No__t_1 メソッドまたは `Next` メソッド (VisualStudio 名前空間) のいずれかから返された `IUnknown` インターフェイスの解釈は、テーブルの種類によって異なります。 たとえば、`IDiaTable` インターフェイスが挿入されたソースの一覧を表す場合は、 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)インターフェイスに対して `IUnknown` インターフェイスを照会する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、 [IDiaEnumTables:: Item](../../debugger/debug-interface-access/idiaenumtables-item.md)または[IDiaEnumTables:: Next](../../debugger/debug-interface-access/idiaenumtables-next.md)メソッドを呼び出します。

次のインターフェイスは `IDiaTable` インターフェイスで実装されます (つまり、次のいずれかのインターフェイスに対して `IDiaTable` インターフェイスに対してクエリを実行できます)。

- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

## <a name="example"></a>例
最初の関数 `ShowTableNames` は、セッション内のすべてのテーブルの名前を表示します。 2番目の関数 `GetTable` は、指定されたインターフェイスを実装するテーブルのすべてのテーブルを検索します。 3番目の関数 `UseTable` は、`GetTable` 関数の使用方法を示しています。

> [!NOTE]
> `CDiaBSTR` は、`BSTR` をラップし、インスタンス化がスコープ外になったときに文字列の解放を自動的に処理するクラスです。

```C++
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

## <a name="requirements"></a>［要件］
ヘッダー: Dia2

ライブラリ: diaguids

DLL: msdia80

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
- [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
