---
title: IDiaLoadCallback |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback interface
ms.assetid: 2f18c64c-2cf0-43fc-a447-21e82702ca2a
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b26a638c1ac8bd808bae6fa78aaa3cc24dedede5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151961"
---
# <a name="idialoadcallback"></a>IDiaLoadCallback
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

DIA シンボル検索プロシージャからコールバックを受信します。これにより、ユーザーインターフェイスは、場所の試行の進行状況についてレポートすることができます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaLoadCallback : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスでは、次のメソッドが公開されています。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)|デバッグディレクトリが .exe ファイルで見つかったときに呼び出されます。|  
|[IDiaLoadCallback::NotifyOpenDBG](../../debugger/debug-interface-access/idialoadcallback-notifyopendbg.md)|Dbg ファイルが開かれたときに呼び出されます。|  
|[IDiaLoadCallback::NotifyOpenPDB](../../debugger/debug-interface-access/idialoadcallback-notifyopenpdb.md)|任意の .pdb ファイルが開かれたときに呼び出されます。|  
|[IDiaLoadCallback::RestrictRegistryAccess](../../debugger/debug-interface-access/idialoadcallback-restrictregistryaccess.md)|シンボル検索パスを検索するためにレジストリクエリを使用できるかどうかを決定します。|  
|[IDiaLoadCallback::RestrictSymbolServerAccess](../../debugger/debug-interface-access/idialoadcallback-restrictsymbolserveraccess.md)|シンボルを解決するために、シンボルサーバーへのアクセスが許可されているかどうかを判断します。|  
  
## <a name="remarks"></a>注釈  
 クライアントアプリケーションは、このインターフェイスを実装し、 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドの呼び出しでこのインターフェイスへの参照を提供します。  
  
 読み込みプロセスに適用できるその他の制限については、 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md) インターフェイスを参照してください。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)   
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)   
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
