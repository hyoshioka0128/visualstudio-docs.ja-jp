---
title: 'IDiaDataSource:: loadDataForExe |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataForExe method
ms.assetid: d94a1068-f53f-44b5-b6fb-00dec361a7f2
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 623cdd74b086a46bc52c0f0534953ae6e11168ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547378"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

を開き、.exe/.dll ファイルに関連付けられているデバッグデータを準備します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT loadDataForExe (  
   LPCOLESTR executable,  
   LPCOLESTR searchPath,  
   IUnknown* pCallback  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 executable  
 から.Exe ファイルまたは .dll ファイルへのパス。  
  
 searchPath  
 からデバッグデータを検索する代替パス。  
  
 pCallback  
 から `IUnknown` [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)、 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)、 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)、 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) の各インターフェイスなど、デバッグコールバックインターフェイスをサポートするオブジェクトのインターフェイスです。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、このメソッドで使用できるエラーコードをいくつか示します。  
  
|値|説明|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|ファイルを開くことができませんでした。または、ファイルの形式が無効です。|  
|E_PDB_FORMAT|古い形式のファイルにアクセスしようとしました。|  
|E_PDB_INVALID_SIG|署名が一致しません。|  
|E_PDB_INVALID_AGE|年齢が一致しません。|  
|E_INVALIDARG|無効なパラメーター。|  
|E_UNEXPECTED|データソースは既に準備されています。|  
  
## <a name="remarks"></a>注釈  
 .Exe/.dll ファイルのデバッグヘッダーは、関連付けられたデバッグデータの場所に名前を付けます。  
  
 このメソッドは、デバッグヘッダーを読み取り、デバッグデータを検索して準備します。 検索の進行状況は、必要に応じて、コールバックを使用して報告および制御することができます。 たとえば、 [IDiaLoadCallback:: NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md) は、 `IDiaDataSource::loadDataForExe` メソッドがデバッグディレクトリを検出して処理するときに呼び出されます。  
  
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)インターフェイスと[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)インターフェイスを使用すると、標準のファイル i/o を通じて直接ファイルにアクセスできない場合に、クライアントアプリケーションが実行可能ファイルからデータを読み取るための別の方法を提供できます。  
  
 検証せずに .pdb ファイルを読み込むには、 [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) メソッドを使用します。  
  
 特定の条件に対して .pdb ファイルを検証するには、 [IDiaDataSource:: loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) メソッドを使用します。  
  
 メモリから .pdb ファイルを直接読み込むには、 [IDiaDataSource:: loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) メソッドを使用します。  
  
## <a name="example"></a>例  
  
```cpp#  
class MyCallBack: public IDiaLoadCallback  
{  
...  
};  
MyCallBack callback;  
...  
HRESULT hr = pSource->loadDataForExe( L"myprog.exe", L".\debug", (IUnknown*)&callback);  
if (FAILED(hr))  
{  
    // Report error  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)   
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)   
 [IDiaLoadCallback:: NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)   
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)   
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)   
 [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource:: loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
