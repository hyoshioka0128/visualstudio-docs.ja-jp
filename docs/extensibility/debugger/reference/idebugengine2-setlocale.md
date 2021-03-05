---
description: デバッグエンジン (DE) のロケールを設定します。
title: 'IDebugEngine2:: SetLocale |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetLocale
helpviewer_keywords:
- IDebugEngine2::SetLocale
ms.assetid: cd0d2cf1-2aac-43da-a830-4bb3d696c219
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 54cfd2d9d51cbad414cfb481b88f1e3277500efa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153912"
---
# <a name="idebugengine2setlocale"></a>IDebugEngine2::SetLocale
デバッグエンジン (DE) のロケールを設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetLocale( 
   WORD wLangID
);
```

```csharp
int SetLocale( 
   ushort wLangID
);
```

## <a name="parameters"></a>パラメーター
`wLangID`\
から言語のロケールを指定します。 たとえば、英語の場合は1033です。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、セッションデバッグマネージャー (SDM) によって呼び出され、DE によって返される文字列が適切にローカライズされるように、IDE のロケール設定を伝達します。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
