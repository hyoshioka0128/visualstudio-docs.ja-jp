---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7379436ae0da57d7f8c47ce8484c810a53a0a453
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723357"
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

## <a name="remarks"></a>注釈
 渡されるインターフェイス `pSession` は、クッキーとしてのみ扱われます。これは、最初にこのプロセスにアタッチされたセッションデバッグマネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
