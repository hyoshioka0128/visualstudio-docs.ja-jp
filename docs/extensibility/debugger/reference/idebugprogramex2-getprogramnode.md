---
description: プログラムに関連付けられているプログラムノードを取得します。
title: 'IDebugProgramEx2:: GetProgramNode |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 1545ffbf-1422-4b5d-9bb9-314ba8665041
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 10e96e69459e591567b873e6268a29249439210a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084065"
---
# <a name="idebugprogramex2getprogramnode"></a>IDebugProgramEx2::GetProgramNode
プログラムに関連付けられているプログラムノードを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProgramNode( 
   IDebugProgramNode2** ppProgramNode
);
```

```csharp
int GetProgramNode( 
   out IDebugProgramNode2 ppProgramNode
);
```

## <a name="parameters"></a>パラメーター
`ppProgramNode`\
入出力このプログラムに関連付けられているプログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
