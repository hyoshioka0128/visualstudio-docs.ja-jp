---
description: PDB ファイルに格納されているソースサーバー情報を表します。
title: IDebugSourceServerModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSourceServerModule interface
ms.assetid: 38213060-451d-46e6-8b4a-efc123e01a2c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5b12e93d52fe841b66baae341a6854e0217dcb00
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071169"
---
# <a name="idebugsourceservermodule"></a>IDebugSourceServerModule
PDB ファイルに格納されているソースサーバー情報を表します。

## <a name="syntax"></a>Syntax

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

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
