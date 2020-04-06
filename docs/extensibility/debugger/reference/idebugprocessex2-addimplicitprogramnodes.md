---
title: IデバッグプロセスEx2::アプリシプリシブルプログラムノードを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 113c81e95e7384be04b7e02a5c58cd2cad7c9c6b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723399"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
このメソッドは、指定された各デバッグ エンジン (DE) のプログラム ノードを追加します。

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
[in]プログラム`GUID`の起動に使用される DE の (および独自のプログラム ノードを追加すると想定される) の。

`rgguidSpecificEngines`\
[in]プログラム`GUID`ノードが追加される D の配列。

`celtSpecificEngines`\
[in]配列内の`GUID`s`rgguidSpecificEngines`の数。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
- [プログラムノード](../../../extensibility/debugger/program-nodes.md)は、プログラムの起動時に独自の`rgguidSpecificEngines`プログラムノードを追加すると想定される起動エンジンを`guidLaunchingEngine`除いて、(に示されている)に示された各DEに追加されます。

## <a name="see-also"></a>関連項目
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [プログラム ノード](../../../extensibility/debugger/program-nodes.md)
