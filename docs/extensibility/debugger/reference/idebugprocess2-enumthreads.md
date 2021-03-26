---
description: プロセスで実行されているすべてのスレッドの一覧を取得します。
title: 'IDebugProcess2:: EnumThreads |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6c502504b3a31f3e4689db34f907f9596b214877
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071611"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
プロセスで実行されているすべてのスレッドの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumThreads(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int EnumThreads(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力プロセス内のすべてのプログラム内のすべてのスレッドの一覧を含む [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、各プログラムで実行されているスレッドを列挙し、それらをスレッドのプロセスビューに結合します。 1つのスレッドが複数のプログラムで実行される場合があります。このメソッドは、そのスレッドを1回だけ列挙します。

 このメソッドは、重複しないプロセスのスレッドの一覧を表示します。 それ以外の場合、特定のプログラムで実行されているスレッドを列挙するには、 [Enumthreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) メソッドを使用します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
