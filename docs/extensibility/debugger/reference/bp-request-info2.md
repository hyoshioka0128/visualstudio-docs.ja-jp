---
title: BP_REQUEST_INFO2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04d1db2ca8176678d8a72a84ede2bddcbfa2f152
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737882"
---
# <a name="bp_request_info2"></a>BP_REQUEST_INFO2
ブレークポイントの実装に必要な情報 (ベンダー GUID、制約、トレース ポイントなど) が含まれます。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_REQUEST_INFO2 {
    BPREQI_FIELDS   dwFields;
    GUID            guidLanguage;
    BP_LOCATION     bpLocation;
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    IDebugThread2*  pThread;
    BSTR            bstrThreadName;
    BP_CONDITION    bpCondition;
    BP_PASSCOUNT    bpPassCount;
    BP_FLAGS        dwFlags;
    GUID            guidVendor;
    BSTR            bstrConstraint;
    BSTR            bstrTracepoint;
} BP_REQUEST_INFO2;
```

```csharp
public struct BP_REQUEST_INFO2 {
    public uint           dwFields;
    public Guid           guidLanguage;
    public BP_LOCATION    bpLocation;
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public IDebugThread2  pThread;
    public string         bstrThreadName;
    public BP_CONDITION   bpCondition;
    public BP_PASSCOUNT   bpPassCount;
    public uint           dwFlags;
    public Guid           guidVendor;
    public string         bstrConstraint;
    public string         bstrTracepoint;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)列挙体のフラグの組み合わせ。

`guidLanguage`\
言語の GUID です。

`bpLocation`\
ブレークポイントの場所の種類を指定する[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造体。

`pProgram`\
ブレークポイントが発生するアプリケーションを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。

`bstrProgramName`\
ブレークポイントが発生するアプリケーションの名前。

`pThread`\
ブレークポイントが発生するスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

`bstrThreadName`\
ブレークポイントが発生するスレッドの名前。

`bpCondition`\
ブレークポイントが発生する条件を記述する[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)構造体。

`bpPassCount`\
ブレークポイントのパス カウント情報を含む[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)構造体。

`dwFlags`\
要求されたブレークポイントのフラグを指定する[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)列挙体のフラグの組み合わせ。

`guidVendor`\
仕入先の GUID です。 NULL 値である可能性があります。

`bstrConstraint`\
ブレークポイント制約の名前。 NULL 値である可能性があります。

`bstrTracepoint`\
トレース ポイントの名前。 NULL 値である可能性があります。

## <a name="remarks"></a>Remarks
この構造体は[、GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
