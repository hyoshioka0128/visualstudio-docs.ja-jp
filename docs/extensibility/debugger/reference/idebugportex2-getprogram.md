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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5bb169ecdbd0dcea188054c96af06da609edf3f7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142805"
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

## <a name="see-also"></a>関連項目
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
