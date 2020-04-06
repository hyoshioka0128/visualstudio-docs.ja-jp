---
title: をクリックします。マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719912"
---
# <a name="idebugsourceservermodule"></a>IDebugSourceServerModule
PDB ファイルに含まれるソース サーバー情報を表します。

## <a name="syntax"></a>構文

```
IDebugSourceServerModule : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、デバッガー エンジンによって実装され、デバッガー UI によって使用されます。

## <a name="methods"></a>メソッド
 次の表に`IDebugSourceServerModule`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetSourceServerData](../../../extensibility/debugger/reference/idebugsourceservermodule-getsourceserverdata.md)|ソース サーバー情報の配列を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:
