---
title: IDebugSourceServerModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSourceServerModule interface
ms.assetid: 38213060-451d-46e6-8b4a-efc123e01a2c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a2c362bc4a103c707238acfa3b3148f00c0e25be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719912"
---
# <a name="idebugsourceservermodule"></a>IDebugSourceServerModule
PDB ファイルに格納されているソースサーバー情報を表します。

## <a name="syntax"></a>構文

```
IDebugSourceServerModule : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスはデバッガーエンジンによって実装され、デバッガー UI によって使用されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugSourceServerModule` ます。

|メソッド|説明|
|------------|-----------------|
|[GetSourceServerData](../../../extensibility/debugger/reference/idebugsourceservermodule-getsourceserverdata.md)|転送元サーバー情報の配列を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
