---
description: プログラムノードに関連付けられているプログラムを取得します。
title: 'IDebugPortEx2:: GetProgram |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::GetProgram
helpviewer_keywords:
- IDebugPortEx2::GetProgram
ms.assetid: cd83a111-bfd5-4eae-b576-526466c6b6ec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4efdd9c5a70849a6df1aefb95db384e3dd60f057
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072508"
---
# <a name="idebugportex2getprogram"></a>IDebugPortEx2::GetProgram
プログラムノードに関連付けられているプログラムを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProgram( 
   IDebugProgramNode2* pProgramNode,
   IDebugProgram2**    ppProgram
);
```

```csharp
int GetProgram( 
   IDebugProgramNode2 pProgramNode,
   out IDebugProgram2 ppProgram
);
```

## <a name="parameters"></a>パラメーター
`pProgramNode` からプログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクト。

`ppProgram` 入出力プログラムノードに関連付けられているプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
