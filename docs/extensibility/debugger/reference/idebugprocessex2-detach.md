---
description: このメソッドは、セッションがプロセスのデバッグを終了したことをプロセスに通知します。
title: IDebugProcessEx2::D etach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Detach
helpviewer_keywords:
- IDebugProcessEx2::Detach method
ms.assetid: 66d54c2c-9302-47c8-9975-f30ed988ab29
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3140da647b46a1cbc3b60691e820238c2c6c83eb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166256"
---
# <a name="idebugprocessex2detach"></a>IDebugProcessEx2::Detach
このメソッドは、セッションがプロセスのデバッグを終了したことをプロセスに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT Detach( 
   IDebugSession2* pSession
);
```

```csharp
int Detach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>パラメーター
`pSession`\
からこのプロセスをデタッチするセッションを一意に識別する値。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 渡されるインターフェイス `pSession` は、クッキーとしてのみ扱われます。これは、最初にこのプロセスにアタッチされたセッションデバッグマネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
