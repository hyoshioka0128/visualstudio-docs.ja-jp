---
description: モジュールをユーザーコードとしてマークします。
title: 'IDebugModule3:: Setジャスト Mycodestate |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::SetJustMyCodeState
helpviewer_keywords:
- IDebugModule3::SetJustMyCodeState
ms.assetid: 68f8166d-ef64-49ae-ad5e-79604f43bbd4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1e4d1664c17ad9c822990ea8b3ef8c2bc0c3c664
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149881"
---
# <a name="idebugmodule3setjustmycodestate"></a>IDebugModule3::SetJustMyCodeState
モジュールをユーザーコードとしてマークします。

## <a name="syntax"></a>構文

```cpp
HRESULT SetJustMyCodeState(
   BOOL fIsUserCode
);
```

```csharp
int SetJustMyCodeState(
   int fIsUserCode
);
```

## <a name="parameters"></a>パラメーター
`fIsUserCode`\
からモジュールを `TRUE` ユーザーコードと見なす場合は0以外 ()。それ以外の場合は 0 ( `FALSE` )。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
