---
title: 'IDebugProcessEx2:: AddImplicitProgramNodes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8ef9379edc9e02e8bed6761abf0aa4a2830fc415
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861089"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
このメソッドは、指定された各デバッグエンジン (DE) のプログラムノードを追加します。

## <a name="syntax"></a>構文

```cpp
HRESULT AddImplicitProgramNodes(
   REFGUID guidLaunchingEngine,
   GUID*   rgguidSpecificEngines,
   DWORD   celtSpecificEngines
);
```

```csharp
int AddImplicitProgramNodes(
   ref Guid guidLaunchingEngine,
   Guid[]   rgguidSpecificEngines,
   uint     celtSpecificEngines
);
```

## <a name="parameters"></a>パラメーター
`guidLaunchingEngine`\
からプログラムを起動するために使用される `GUID` (および、独自のプログラムノードを追加すると想定される) の。

`rgguidSpecificEngines`\
から `GUID`プログラムノードが追加される DEs のの配列。

`celtSpecificEngines`\
から配列内のの数 `GUID` `rgguidSpecificEngines` 。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
- に示されている各 DE に対して[プログラムノード](../../../extensibility/debugger/program-nodes.md)が追加されます。これは、 `rgguidSpecificEngines` `guidLaunchingEngine` プログラムを起動したときに、独自のプログラムノードを追加することを前提としています (で指定されているように)。

## <a name="see-also"></a>関連項目
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [プログラム ノード](../../../extensibility/debugger/program-nodes.md)
