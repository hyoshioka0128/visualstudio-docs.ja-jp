---
description: このプログラムが実行されているプロセスを取得します。
title: 'IDebugProgram2:: GetProcess |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 233bd9bbb41f64b375e899dba9c0be9a9fba3d97
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168990"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
このプログラムが実行されているプロセスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProcess(
   IDebugProcess2** ppProcess
);
```

```csharp
int GetProcess(
   out IDebugProcess2 ppProcess
);
```

## <a name="parameters"></a>パラメーター
`ppProcess`\
入出力プロセスを表す [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 デバッグエンジン (DE) が [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md) インターフェイスを実装していない限り、このメソッドの de 実装は常にを返す必要があります。これは、de が実行している `E_NOTIMPL` プロセスを特定できないため、このメソッドの実装を満たすことができないためです。

 インターフェイスを実装することは `IDebugEngineLaunch2` 、プロセスの作成方法を de が知る必要があることを意味します。したがって、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスの de 実装では、実行されているプロセスを知ることができます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
