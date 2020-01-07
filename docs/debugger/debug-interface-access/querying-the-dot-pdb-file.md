---
title: に対するクエリを実行しています。Pdb ファイル |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68efbd59abe1b0aff717a55383f3ac330586164a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738580"
---
# <a name="querying-the-pdb-file"></a>.Pdb ファイルの照会
プログラムデータベースファイル (拡張子 .pdb) は、プロジェクトのコンパイルとリンクの過程で収集された型とシンボリックデバッグ情報を含むバイナリファイルです。 PDB ファイルは、 **/zi**または **/zi**を使用しC++て C/プログラムをコンパイルするか、 **/debug**オプションを使用して [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]、または [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] プログラムをコンパイルすると作成されます。 オブジェクトファイルには、デバッグ情報の .pdb ファイルへの参照が含まれています。 Pdb ファイルの詳細については、「 [Pdb ファイル](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100))」を参照してください。 DIA アプリケーションでは、次の一般的な手順を使用して、実行可能イメージ内のさまざまなシンボル、オブジェクト、およびデータ要素の詳細を取得できます。

### <a name="to-query-the-pdb-file"></a>.Pdb ファイルに対してクエリを実行するには

1. [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)インターフェイスを作成して、データソースを取得します。

    ```C++
    CComPtr<IDiaDataSource> pSource;
    hr = CoCreateInstance( CLSID_DiaSource,
                           NULL,
                           CLSCTX_INPROC_SERVER,
                           __uuidof( IDiaDataSource ),
                          (void **) &pSource);

    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    ```

2. [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)または[IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)を呼び出して、デバッグ情報を読み込みます。

    ```C++
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename, szFilename, sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    ```

3. [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)を呼び出して[IDiaSession](../../debugger/debug-interface-access/idiasession.md)を開き、デバッグ情報にアクセスできるようにします。

    ```C++
    CComPtr<IDiaSession> psession;
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
    ```

4. @No__t_0 のメソッドを使用して、データソース内のシンボルを照会します。

    ```C++
    CComPtr<IDiaSymbol> pglobal;
    if ( FAILED( psession->get_globalScope( &pglobal) ) )
    {
        Fatal( "get_globalScope" );
    }
    ```

5. @No__t_0 インターフェイスを使用して、シンボルやデバッグ情報のその他の要素を列挙し、スキャンします。

    ```C++
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) ) && celt == 1 )
    {
        // Do something with each IDiaTable.
    }
    ```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
