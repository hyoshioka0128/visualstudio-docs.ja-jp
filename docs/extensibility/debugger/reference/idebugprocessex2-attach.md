---
title: を使用して処理を行います。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Attach
helpviewer_keywords:
- IDebugProcessEx2::Attach method
ms.assetid: f3334ed7-39bf-4d02-a338-36f567b9b287
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d70da2530a1677367a22968436a17eba809fd24a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723387"
---
# <a name="idebugprocessex2attach"></a>IDebugProcessEx2::Attach
このメソッドは、セッションがプロセスをデバッグしていることをプロセスに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugSession2* pSession
);
```

```csharp
int Attach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>パラメーター
`pSession`\
[in]このプロセスにアタッチするセッションを一意に識別する値。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 渡される`pSession`インターフェイスは、Cookie としてのみ扱われるため、このプロセスにアタッチするセッション デバッグ マネージャーを一意に識別する値です。指定されたインターフェイス上のメソッドはどれも機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
