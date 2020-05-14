---
title: Iデバッグスキャンストップイベント2::CanStop |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2915938c966bac7f842d0745c973c7d0b7033e2b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734594"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
現在のコードの場所で停止するか、または実行を続行するかのどちらをデバッグ エンジン (DE) に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanStop ( 
   BOOL fCanStop
);
```

```csharp
int CanStop ( 
   int fCanStop
);
```

## <a name="parameters"></a>パラメーター
`fCanStop`\
[in]DE が現在`TRUE`のコード位置で停止する必要がある場合は、非ゼロ ( ) 。それ以外の場合`FALSE`は、ゼロ ( ) 。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 通常、このイベントの受信側は[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)メソッドを呼び出して DE が停止する理由を`IDebugCanStopEvent2::CanStop`判断し、適切な応答を使用してメソッドを呼び出します。

 DE が停止すると、停止の理由を説明するイベントが送信されます。 通常、送信されるイベントは 2 つあり、ユーザーまたはシグナルブレークは[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)インターフェイスによって表され、ブレークポイント イベントは[、IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
