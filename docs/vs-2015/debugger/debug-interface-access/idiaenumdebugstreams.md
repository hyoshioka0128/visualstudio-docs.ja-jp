---
title: IDiaEnumDebugStreams |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams interface
ms.assetid: 611caf4f-7a5f-4aa4-b909-52feeb3cc752
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b56170ce1551f4443d511d4b6fde6c5d177d9c21
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182514"
---
# <a name="idiaenumdebugstreams"></a>IDiaEnumDebugStreams
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

データソースに格納されているさまざまなデバッグストリームを列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaEnumDebugStreams : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDiaEnumDebugStreams` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaEnumDebugStreams::get__NewEnum](../../debugger/debug-interface-access/idiaenumdebugstreams-get-newenum.md)|`IEnumVARIANT`この列挙子のバージョンを取得します。|  
|[IDiaEnumDebugStreams::get_Count](../../debugger/debug-interface-access/idiaenumdebugstreams-get-count.md)|デバッグストリームの数を取得します。|  
|[IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md)|インデックスを使ってデバッグストリームを取得します。|  
|[IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)|列挙シーケンス内の指定された数のデバッグストリームを取得します。|  
|[IDiaEnumDebugStreams::Skip](../../debugger/debug-interface-access/idiaenumdebugstreams-skip.md)|列挙シーケンス内の指定された数のデバッグストリームをスキップします。|  
|[IDiaEnumDebugStreams::Reset](../../debugger/debug-interface-access/idiaenumdebugstreams-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[IDiaEnumDebugStreams::Clone](../../debugger/debug-interface-access/idiaenumdebugstreams-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
  
## <a name="remarks"></a>注釈  
 デバッグストリームの内容は実装に依存し、データ形式は文書化されていません。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 オブジェクトを取得するには、 [IDiaSession:: getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md) メソッドを呼び出し `IDiaEnumDebugStreams` ます。  
  
## <a name="example"></a>例  
 この例では、このインターフェイスから使用可能なデータストリームにアクセスする方法を示します。 関数の実装については、 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md) インターフェイスを参照してください `PrintStreamData` 。  
  
```cpp#  
void DumpAllDebugStreams( IDiaSession* pSession)  
{  
    IDiaEnumDebugStreams* pEnumStreams;  
  
    wprintf(L"\n\n*** DEBUG STREAMS\n\n");  
    // Retrieve an enumerated sequence of debug data streams  
    if(pSession->getEnumDebugStreams(&pEnumStreams) == S_OK)  
    {  
        IDiaEnumDebugStreamData* pStream;  
        ULONG celt = 0;  
  
        for(; pEnumStreams->Next(1, &pStream, &celt) == S_OK; pStream = NULL)  
        {  
            PrintStreamData(pStream);  
            pStream->Release();  
        }  
        pEnumStreams->Release();  
    }  
    else  
    {  
      wprintf(L"Failed to get any debug streams!\n");  
    }  
    wprintf(L"\n");  
}  
```  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)   
 [IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)
