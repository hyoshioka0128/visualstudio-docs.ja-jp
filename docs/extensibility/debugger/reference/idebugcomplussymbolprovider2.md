---
title: IDebugComPlusSymbolProvider2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider2 interface
ms.assetid: fa2f9b49-03ad-43c7-92d6-6dcb9c3d0531
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28c68398b69196f53c4f8792f3479d403cbebcda
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80733234"
---
# <a name="idebugcomplussymbolprovider2"></a>IDebugComPlusSymbolProvider2
マネージコードに固有のメソッドを持ち、 **IDebugComPlusSymbolProvider**[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)を拡張する com + シンボルプロバイダーを表します。

## <a name="syntax"></a>構文

```
IDebugComPlusSymbolProvider2 : IDebugComPlusSymbolProvider
```

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[FunctionHasLineInfo](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-functionhaslineinfo.md)|指定したメソッドに行情報があるかどうかを判断します。|
|[GetTypesByName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-gettypesbyname.md)|名前を指定して型を取得します。|
|[GetTypeFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-gettypefromtoken.md)|トークンを指定して型を取得します。|
|[IsAddressSequencePoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-isaddresssequencepoint.md)|指定されたデバッグアドレスがシーケンスポイントであるかどうかを判断します。|
|[LoadSymbolsFromCallback](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromcallback.md)|指定されたコールバックメソッドを使用してデバッグシンボルを読み込みます。|
|[LoadSymbolsFromStreamWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromstreamwithcormodule.md)|コードオブジェクトを指定し **て、データ** ストリームからデバッグシンボルを読み込みます。|
|[LoadSymbolsWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolswithcormodule.md)|は、コードオブジェクトを **指定して** デバッグシンボルを読み込みます。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
