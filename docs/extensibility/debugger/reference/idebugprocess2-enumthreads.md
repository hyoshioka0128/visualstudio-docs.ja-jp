---
title: IDebugプロセス2::列挙スレッド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 52383649fc45eae6bbac6831f9bb233b9c0a2fde
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724059"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
プロセスで実行されているすべてのスレッドの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumThreads(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int EnumThreads(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[アウト]プロセス内のすべてのプログラムのすべてのスレッドの一覧を含む[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、各プログラムで実行されているスレッドを列挙し、それらを結合してスレッドのプロセス ビューを作成します。 1 つのスレッドが複数のプログラムで実行される場合があります。このメソッドは、そのスレッドを 1 回だけ列挙します。

 このメソッドは、重複のないプロセスのスレッドのリストを表示します。 それ以外の場合は、特定のプログラムで実行されているスレッドを列挙するには[、EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)メソッドを使用します。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
