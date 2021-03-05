---
description: このプログラムの GUID を取得します。
title: 'IDebugProgram2:: GetProgramId |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProgramId
helpviewer_keywords:
- IDebugProgram2::GetProgramId
ms.assetid: 2c31c0aa-2b71-46c7-849c-356e237d26f8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45721d4214c396f3366bd23c2bc48e74a1427ec8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168964"
---
# <a name="idebugprogram2getprogramid"></a>IDebugProgram2::GetProgramId
このプログラムの GUID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProgramId( 
   GUID* pguidProgramId
);
```

```csharp
int GetProgramId( 
   out Guid pguidProgramId
);
```

## <a name="parameters"></a>パラメーター
`pguidProgramId`\
入出力 `GUID` このプログラムのを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 デバッグエンジン (DE) は、最初に [onattach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドまたは [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドに渡されたプログラム id を返す必要があります。 これにより、デバッガーコンポーネント間でプログラムを識別できます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
