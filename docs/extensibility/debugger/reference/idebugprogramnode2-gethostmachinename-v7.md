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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a8c328c83ebe52f842b1990debe07aed3fd764c1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722085"
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

## <a name="remarks"></a>注釈

> [!WARNING]
> Visual Studio 2005 の時点では、このメソッドは使用されなくなり、常にを返す必要があり `E_NOTIMPL` ます。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
