---
title: 'IDebugProgramNodeAttach2:: OnAttach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f61a0629ede07b5b6a4e884157dacaea244c2344
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898483"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
関連付けられているプログラムにアタッチするか、アタッチプロセスを [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドに従います。

## <a name="syntax"></a>構文

```cpp
HRESULT OnAttach(
   [in] REFGUID guidProgramId
);
```

```csharp
int OnAttach(
   ref Guid guidProgramId
};
```

## <a name="parameters"></a>パラメーター
`guidProgramId`\
[入力] `GUID` 関連付けられたプログラムに割り当てる場合は。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE` [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドを呼び出さない場合は、を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 [Attach メソッドが](../../../extensibility/debugger/reference/idebugengine2-attach.md)呼び出される前に、アタッチ処理中にこのメソッドが呼び出されます。 メソッドは、 `OnAttach` アタッチプロセス自体を実行できます (この場合、このメソッドはを返し `S_FALSE` ます)。また、メソッドにアタッチプロセスを遅延させ `IDebugEngine2::Attach` `OnAttach` ます (メソッドはを返し `S_OK` ます)。 どちらの場合も、 `OnAttach` メソッドは、 `GUID` デバッグされているプログラムのを指定されたに設定でき `GUID` ます。

## <a name="see-also"></a>関連項目
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
