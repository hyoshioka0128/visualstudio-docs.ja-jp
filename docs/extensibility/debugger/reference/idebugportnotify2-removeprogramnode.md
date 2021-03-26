---
description: デバッグ可能なプログラムを、実行中のポートから登録解除します。
title: 'IDebugPortNotify2:: RemoveProgramNode |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2::RemoveProgramNode
helpviewer_keywords:
- IDebugPortNotify2::RemoveProgramNode
ms.assetid: 3668157b-66d2-416e-a359-fc04dcd18a48
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 10208570237de10f9a6e682fc3a7478bd15ca24d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072417"
---
# <a name="idebugportnotify2removeprogramnode"></a>IDebugPortNotify2::RemoveProgramNode
デバッグ可能なプログラムを、実行中のポートから登録解除します。

## <a name="syntax"></a>構文

```cpp
HRESULT RemoveProgramNode( 
   IDebugProgramNode2* pProgramNode
);
```

```csharp
int RemoveProgramNode( 
   IDebugProgramNode2 pProgramNode
);
```

## <a name="parameters"></a>パラメーター
`pProgramNode`\
から登録を解除するプログラムを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、 [Addprogramnode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) メソッドを呼び出すことによって追加されたプログラムノードを削除します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
