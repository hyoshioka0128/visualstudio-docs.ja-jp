---
title: 'IDebugProgramNode2:: GetHostMachineName_V7 |Microsoft Docs'
description: これは、Visual Studio 2005 より前に使用されていたホストコンピューター名を取得するための、従来の非推奨のメソッドです。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20d62c180848c4875fa3312e0194ebdb467a93ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053543"
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

## <a name="see-also"></a>こちらもご覧ください

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
