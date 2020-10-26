---
title: IDiaSession |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 002e7198210e123fc2461f712bb8db442b9f25c8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190714"
---
# <a name="idiasession"></a>IDiaSession
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグシンボルのクエリコンテキストを提供します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaSession : IUnknown  
```  
  
## <a name="methods"></a>メソッド  
 次の表に、のメソッドを示し `IDiaSession` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|このシンボルストア内のシンボルに対応する実行可能ファイルの読み込みアドレスを取得します。 これは、メソッドに渡された値と同じです `put_loadAddress` 。|  
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|このシンボルストア内のシンボルに対応する実行可能ファイルの読み込みアドレスを設定します。 **注:**  オブジェクトを取得 `IDiaSession` し、オブジェクトの使用を開始する前に、このメソッドを呼び出すことが重要です。|  
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|グローバルスコープへの参照を取得します。|  
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|シンボルストアに格納されているすべてのテーブルの列挙子を取得します。|  
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|静的な場所にあるすべての名前付きシンボルの列挙子を取得します。|  
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|名前と記号の種類に一致する指定された親識別子のすべての子を取得します。|  
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|指定したアドレスを含む、またはそれに最も近いシンボルの種類を取得します。|  
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|指定した相対仮想アドレス (RVA) を含む、またはそれに最も近いシンボルの種類を取得します。|  
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|指定した仮想アドレス (VA) を含む、またはそれに最も近いシンボルの種類を取得します。|  
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|指定したメタデータトークンを含むシンボルを取得します。|  
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|2つの記号が等しいかどうかを確認します。|  
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|一意の識別子によって記号を取得します。|  
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|指定した相対仮想アドレスとオフセットを格納している、またはそれに最も近いシンボルの種類を取得します。|  
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|指定した仮想アドレスとオフセットを格納している、またはそれに最も近いシンボルの種類を取得します。|  
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|コンパイル単位と名前を指定してソースファイルを取得します。|  
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|ソースファイル識別子でソースファイルを取得します。|  
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|指定したコンパイル単位とソースファイル識別子内の行番号を取得します。|  
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|指定したアドレスを含む、指定したコンパイル単位内の行を取得します。|  
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|指定した相対仮想アドレスを含む、指定したコンパイル単位内の行を取得します。|  
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|指定されたアドレス範囲に含まれる行の行番号の情報を検索します。|  
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|ソースファイルと行番号を指定して、指定したコンパイル単位の行を取得します。|  
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|属性プロバイダーまたはコンパイルプロセスの他のコンポーネントによってシンボルストアに配置されたソースを取得します。|  
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|デバッグデータストリームの列挙シーケンスを取得します。|  
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|指定されたアドレスのすべてのインラインフレームをクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|指定した相対仮想アドレス (RVA) のすべてのインラインフレームをクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|指定された仮想アドレス (VA) 上のすべてのインラインフレームをクライアントが反復処理できるようにする列挙を取得します。|  
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|指定した親シンボルによってインラインで、直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|クライアントが、指定された親シンボルによって直接または間接的にインライン化されているすべての関数の行番号情報を反復処理できるようにする列挙体を取得します。指定したアドレス範囲内に含まれます。|  
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|指定された親シンボルによって直接または間接的にインライン化され、指定された相対仮想アドレス (RVA) 内に含まれているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|クライアントが、指定された親シンボルによって直接または間接的にインライン化されているすべての関数の行番号情報を反復処理できるようにする列挙体を取得します。指定した仮想アドレス (VA) 内に含まれます。|  
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|指定したソースファイルと行番号で、直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|指定した名前に一致するすべてのインライン関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|親アクセラレータスタブ関数で、指定したタグ値が対応する変数のシンボルの列挙体を返します。|  
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|このメソッドは、対応するタグ値を指定して、指定された相対仮想アドレスで、指定された親アクセラレータのスタブ関数に含まれるシンボルの列挙体を返します。|  
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|指定されたインライン関数名に対応するインラインフレームのシンボルの列挙体を返します。|  
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|指定したソースの場所に対応するインラインフレームのシンボルの列挙体を返します。|  
  
## <a name="remarks"></a>注釈  
 オブジェクトを作成した後に [IDiaSession::p ut_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) メソッドを呼び出すことが重要です。この `IDiaSession` メソッドに渡される値は `put_loadAddress` 0 以外にする必要があります。これは、シンボルの任意の仮想アドレス (VA) プロパティにアクセスできるようにするためです。 読み込みアドレスは、デバッグ対象の実行可能ファイルが読み込まれたプログラムから取得されます。 たとえば、実行可能ファイルへのハンドルを指定すると、Win32 関数を呼び出して、 `GetModuleInformation` 実行可能ファイルの読み込みアドレスを取得できます。  
  
## <a name="example"></a>例  
 この例では `IDiaSession` 、DIA SDK の一般的な初期化の一部としてインターフェイスを取得する方法を示します。  
  
```cpp#  
CComPtr<IDiaDataSource> pSource;  
ComPtr<IDiaSession> psession;  
  
void InitializeDIA(const char *szFilename)  
{  
    HRESULT hr = CoCreateInstance( CLSID_DiaSource,  
                                   NULL,  
                                   CLSCTX_INPROC_SERVER,  
                                   __uuidof( IDiaDataSource ),  
                                  (void **) &pSource);  
    if (FAILED(hr))  
    {  
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );  
    }  
    wchar_t wszFilename[ _MAX_PATH ];  
    mbstowcs( wszFilename,  
              szFilename,  
              sizeof( wszFilename )/sizeof( wszFilename[0] ) );  
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )  
    {  
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )  
        {  
            Fatal( "loadDataFromPdb/Exe" );  
        }  
    }  
    if ( FAILED( pSource->openSession( &psession ) ) )  
    {  
        Fatal( "openSession" );  
    }  
}  
```  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [Excel.exe](../../debugger/debug-interface-access/exe.md)   
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)   
 [IDiaSymbol:: findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)   
 [.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
