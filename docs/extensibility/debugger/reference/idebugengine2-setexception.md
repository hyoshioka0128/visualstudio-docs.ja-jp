---
description: 特定の例外をデバッグエンジン (DE) でどのように処理するかを指定します。
title: 'IDebugEngine2:: SetException |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetException
helpviewer_keywords:
- IDebugEngine2::SetException
ms.assetid: e6f5ec48-09e8-4b9b-9dc9-55f8d883f1b7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 543cccbbefd12accd75213f255f8e3b677cdea38
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153939"
---
# <a name="idebugengine2setexception"></a>IDebugEngine2::SetException
特定の例外をデバッグエンジン (DE) でどのように処理するかを指定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int SetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>パラメーター
`pException`\
から例外とそのデバッグ方法を説明する [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 例外が発生した場合、初回の場合は例外を生成しないようにします。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
