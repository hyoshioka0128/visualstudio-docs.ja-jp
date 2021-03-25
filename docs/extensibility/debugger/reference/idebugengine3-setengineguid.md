---
description: このメソッドは、デバッグエンジンの (DE) GUID を設定します。
title: 'IDebugEngine3:: SetEngineGuid |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetEngineGuid
helpviewer_keywords:
- IDebugEngine3::SetEngineGuid
ms.assetid: 8bdfa05d-feb7-4d98-abac-77825a04c50f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64d18b8a2cc1e1f0a6ad67418bb4abdf1e684829
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066166"
---
# <a name="idebugengine3setengineguid"></a>IDebugEngine3::SetEngineGuid
このメソッドは、デバッグエンジンの (DE) を設定し `GUID` ます。

## <a name="syntax"></a>構文

```cpp
HRESULT SetEngineGuid(
   GUID* guidEngine
);
```

```csharp
int SetEngineGuid(
   ref Guid guidEngine
);
```

## <a name="parameters"></a>パラメーター
`guidEngine`\
[入力] `GUID` エンジンの。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
