---
title: に対するクエリを実行しています。Pdb ファイル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9b9013d41ac4d5ca890e7cc9e09b5eb9415cb640
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691330"
---
# <a name="querying-the-pdb-file"></a>.Pdb ファイルの照会
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プログラムデータベースファイル (拡張子 .pdb) は、プロジェクトのコンパイルとリンクの過程で収集された型とシンボリックデバッグ情報を含むバイナリファイルです。 PDB ファイルは、 **/zi**または **/zi**を使用して C/c + + プログラムをコンパイルするか [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 、/debug オプションを使用して、、、またはプログラムをコンパイルすると作成され [!INCLUDE[csprcs](../../includes/csprcs-md.md)] [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] ます。 **/debug** オブジェクトファイルには、デバッグ情報の .pdb ファイルへの参照が含まれています。 Pdb ファイルの詳細については、「 [Pdb ファイル](https://msdn.microsoft.com/1761c84e-8c2c-4632-9649-b5f99964ed3f)」を参照してください。 DIA アプリケーションでは、次の一般的な手順を使用して、実行可能イメージ内のさまざまなシンボル、オブジェクト、およびデータ要素の詳細を取得できます。  
  
### <a name="to-query-the-pdb-file"></a>.Pdb ファイルに対してクエリを実行するには  
  
1. [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)インターフェイスを作成して、データソースを取得します。  
  
    ```cpp#  
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
  
    ```cpp#  
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
  
    ```cpp#  
    CComPtr<IDiaSession> psession;  
    if ( FAILED( pSource->openSession( &psession ) ) )   
    {  
        Fatal( "openSession" );  
    }  
    ```  
  
4. のメソッドを使用して、 `IDiaSession` データソース内のシンボルを照会します。  
  
    ```cpp#  
    CComPtr<IDiaSymbol> pglobal;  
    if ( FAILED( psession->get_globalScope( &pglobal) ) )  
    {  
        Fatal( "get_globalScope" );  
    }  
    ```  
  
5. インターフェイスを使用し `IDiaEnum*` て、シンボルやデバッグ情報のその他の要素を列挙し、スキャンします。  
  
    ```cpp#  
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
  
## <a name="see-also"></a>参照  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
