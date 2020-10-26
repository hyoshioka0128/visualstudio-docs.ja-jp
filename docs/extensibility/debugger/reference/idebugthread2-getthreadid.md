---
title: 'IDebugThread2:: GetThreadId |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetThreadId
helpviewer_keywords:
- IDebugThread2::GetThreadId
ms.assetid: db8b1c07-6b86-47f9-b292-bac19c276d36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7788cc09d92ff4c784fbcb7004393fe0d3074c8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718708"
---
# <a name="idebugthread2getthreadid"></a>IDebugThread2::GetThreadId
システムスレッド識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetThreadId (
    DWORD* pdwThreadId
);
```

```csharp
int GetThreadId (
    out uint pdwThreadId
);
```

## <a name="parameters"></a>パラメーター
`pdwThreadId`\
入出力システムスレッド識別子を返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
スレッド ID は、プロセス内の他のすべてのスレッド間でスレッドを識別するために使用されます。

## <a name="example"></a>例
次の例は、IDebugThread2 インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CProgram` います。 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)

```cpp
HRESULT CProgram::GetThreadId(DWORD* pdwThreadId) {
    *pdwThreadId = GetCurrentThreadId();
    return NOERROR;
}
```

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
