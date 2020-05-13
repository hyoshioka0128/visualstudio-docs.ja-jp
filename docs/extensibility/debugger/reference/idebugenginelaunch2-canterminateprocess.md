---
title: IDebugエンジンの起動2:::プロセスを終了する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::CanTerminateProcess
helpviewer_keywords:
- IDebugEngineLaunch2::CanTerminateProcess
ms.assetid: 7973454d-c957-4123-a0ee-80ebcdbbd2d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 91c68e0a0e314015c1f2e6df2a96243c6ce854e7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730563"
---
# <a name="idebugenginelaunch2canterminateprocess"></a>IDebugEngineLaunch2::CanTerminateProcess
プロセスを終了できるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanTerminateProcess ( 
   IDebugProcess2* pProcess
);
```

```csharp
int CanTerminateProcess ( 
   IDebugProcess2 pProcess
);
```

## <a name="parameters"></a>パラメーター
`pProcess`\
[in]終了するプロセスを表す[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 アクセス`S_FALSE`が拒否されたために、エンジンがプロセスを終了できない場合に返します。

## <a name="remarks"></a>Remarks
 このメソッドが戻`S_OK`る場合は[、TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)メソッドを呼び出して、プロセスを実際に終了できます。

## <a name="see-also"></a>関連項目
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)
