---
title: 'IDebugProcessEx2:: Attach |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723387"
---
# <a name="idebugprocessex2attach"></a>IDebugProcessEx2::Attach
このメソッドは、セッションが現在プロセスをデバッグしていることをプロセスに通知します。

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
からこのプロセスにアタッチするセッションを一意に識別する値。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 渡されるインターフェイス `pSession` は、クッキーとしてのみ扱われます。この値は、このプロセスにアタッチするセッションデバッグマネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
