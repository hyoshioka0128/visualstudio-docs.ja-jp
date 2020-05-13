---
title: Iデバッグプログラムノードアタッチ2::オンアタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dfb8a39af3c030dadddcb148a79a96b57f20e183
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721878"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
関連付けられたプログラムにアタッチするか[、Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドへのアタッチ プロセスを延期します。

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
[in]`GUID`をクリックして、関連付けられたプログラムに割り当てます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 Attach`S_FALSE`メソッド[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)を呼び出さない場合に返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは[、Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドが呼び出される前に、アタッチ プロセス中に呼び出されます。 この`OnAttach`メソッドは、アタッチ プロセス自体を実行できます (このメソッドは`S_FALSE`返す) か、アタッチ`IDebugEngine2::Attach`プロセスをメソッド`OnAttach`に遅延`S_OK`させる (メソッドが返す)。 どちらの場合も、メソッド`OnAttach`はデバッグ中の`GUID`プログラムの を指定`GUID`された .

## <a name="see-also"></a>関連項目
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
