---
title: 'IDebugEngine3:: Setジャスト Mycodestate |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e706d0fd23bc0c5388ee3bd6bb82323309725c1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887186"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
このメソッドは、ジャスト Mycode 状態情報についてデバッグエンジンに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetJustMyCodeState(
   BOOL           fUpdate,
   DWORD          dwModules,
   JMC_CODE_SPEC* rgJMCSpec
);
```

```csharp
int SetJustMyCodeState(
   int             fUpdate,
   uint            dwModules,
   JMC_CODE_SPEC[] rgJMCSpec
);
```

## <a name="parameters"></a>パラメーター
`fUpdate`\
から現在の `TRUE` 情報を更新する場合は0以外 ()。すべての情報をリセットする場合は 0 ( `FALSE` )。

`dwModules`\
からの情報構造の数 `rgJMCSpec.`

`rgJMCSpec`\
から使用する [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) 構造体の配列。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 ジャスト Mycode は、システムコードでソースコードを使用できる場合でも、ユーザーに属しているコードのみをデバッグし、システムコードなどのすべての中間コードを無視するという概念です。

## <a name="see-also"></a>関連項目
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)
