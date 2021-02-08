---
title: IDebugSourceServerModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSourceServerModule interface
ms.assetid: 38213060-451d-46e6-8b4a-efc123e01a2c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8dfc4b3defc0b74c1e22c45670209682692a4807
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837698"
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

|Method|説明|
|------------|-----------------|
|[GetSourceServerData](../../../extensibility/debugger/reference/idebugsourceservermodule-getsourceserverdata.md)|転送元サーバー情報の配列を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
