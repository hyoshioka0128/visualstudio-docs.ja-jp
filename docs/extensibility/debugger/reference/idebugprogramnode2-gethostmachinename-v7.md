---
title: 'IDebugProgramNode2:: GetHostMachineName_V7 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 843e5fdf91fe817681b95422474d3887de5756b0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898609"
---
# <a name="idebugprogramnode2gethostmachinename_v7"></a>IDebugProgramNode2::GetHostMachineName_V7

> [!Note]
> れ. 使用しないでください。

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
入出力プログラムが実行されているコンピューターの名前を返します。

## <a name="return-value"></a>戻り値

実装は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="remarks"></a>解説

> [!WARNING]
> Visual Studio 2005 の時点では、このメソッドは使用されなくなり、常にを返す必要があり `E_NOTIMPL` ます。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
