---
title: Iデバッグスキャンストップイベント2::ゲット理由 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59e611c3ed69528f92a6085cf74aa44efed09144
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734525"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
デバッグ エンジン (DE) が停止する理由を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetReason( 
   CANSTOP_REASON* pcr
);
```

```csharp
int GetReason( 
   out enum_CANSTOP_REASON pcr
);
```

## <a name="parameters"></a>パラメーター
`pcr`\
[アウト]このイベントの理由を説明する[CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)列挙体から値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは通常[、CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)メソッドの前に呼び出されるため、呼び出し元`TRUE`は 0`IDebugCanStopEvent2::CanStop`以外のメソッド ( ) を渡すかどうかを判断できます。

 停止の理由は`CANSTOP_ENTRYPOINT`、DE がエントリ ポイントに達したことを意味するか、または`CANSTOP_STEPIN`DE が関数にステップ インしたことを意味します。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)
- [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
