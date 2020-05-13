---
title: IDebugエンジンの起動2::プロセスを終了する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::TerminateProcess
helpviewer_keywords:
- IDebugEngineLaunch2::TerminateProcess
ms.assetid: f7039e7f-5f57-4222-9ad2-11a66b2da6e0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 971259edc89d1ad8be01b6e6e4db46f760534349
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730511"
---
# <a name="idebugenginelaunch2terminateprocess"></a>IDebugEngineLaunch2::TerminateProcess
プロセスを終了します。

## <a name="syntax"></a>構文

```cpp
HRESULT TerminateProcess ( 
   IDebugProcess2* pProcess
);
```

```csharp
int TerminateProcess ( 
   IDebugProcess2 pProcess
);
```

## <a name="parameters"></a>パラメーター
`pProcess`\
[in]終了するプロセスを表す[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出す前に[、メソッドを](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)
