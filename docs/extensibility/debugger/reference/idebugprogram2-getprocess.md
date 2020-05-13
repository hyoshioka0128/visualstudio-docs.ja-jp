---
title: Iデバッグプログラム2::ゲットプロセス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aca1842e92e7e1c164a6468e6c1e94a352ef67c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722784"
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
[アウト]プロセスを表す[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 デバッグ エンジン (DE) が[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)インターフェイスを実装していない限り、DE のこのメソッド`E_NOTIMPL`の実装は、DE が実行されているプロセスを決定できないため、このメソッドの実装を満たすことができないため、常に返す必要があります。

 インターフェイスを`IDebugEngineLaunch2`実装することは、DE がプロセスの作成方法を知っている必要があることを意味します。したがって、DE の[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスの実装は、それが実行されているプロセスを知ることができる。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
