---
description: このメソッドは、すべての未処理の例外の状態を設定します。
title: 'IDebugEngine3:: SetAllExceptions |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetAllExceptions
helpviewer_keywords:
- IDebugEngine3::SetAllExceptions
ms.assetid: 8f03a6ac-a854-42f7-933c-a2df1b351975
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 734a227bbd9387f591314c65be1124d1b2593fd2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153756"
---
# <a name="idebugengine3setallexceptions"></a>IDebugEngine3::SetAllExceptions
このメソッドは、すべての未処理の例外の状態を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetAllExceptions(
   EXCEPTION_STATE dwState
);
```

```csharp
int SetAllExceptions(
   enum_EXCEPTION_STATE dwState
);
```

## <a name="parameters"></a>パラメーター
`dwState`\
から [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) 値の1つ。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
