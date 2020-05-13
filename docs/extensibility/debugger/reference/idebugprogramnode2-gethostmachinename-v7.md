---
title: プログラムノード2::GetHostMachineName_V7 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a8c328c83ebe52f842b1990debe07aed3fd764c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722085"
---
# <a name="idebugprogramnode2gethostmachinename_v7"></a>IDebugProgramNode2::GetHostMachineName_V7

> [!Note]
> 廃止。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostMachineName_V7 (
   BSTR* pbstrHostMachineName
);
```

```csharp
int GetHostMachineName_V7 (
   out string pbstrHostMachineName
);
```

## <a name="parameters"></a>パラメーター

`pbstrHostMachineName`\
[アウト]プログラムが実行されているマシンの名前を返します。

## <a name="return-value"></a>戻り値

実装は常に`E_NOTIMPL`を返す必要があります。

## <a name="remarks"></a>Remarks

> [!WARNING]
> Visual Studio 2005 以降では、このメソッドは使用されなくなり、`E_NOTIMPL`常に を返す必要があります。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
