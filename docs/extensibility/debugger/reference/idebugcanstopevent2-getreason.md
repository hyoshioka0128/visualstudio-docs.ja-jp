---
title: 'IDebugCanStopEvent2:: GetReason |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2aadf18dbf45f8b10791c69ed4f189c38491636d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890293"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
デバッグエンジン (DE) が停止する理由を取得します。

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
入出力このイベントの理由を説明する [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md) 列挙から値を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、通常、呼び出し元がゼロ以外 () をメソッドに渡すかどうかを判断できるように、 [Canstop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) メソッドの前に呼び出され `TRUE` `IDebugCanStopEvent2::CanStop` ます。

 停止の理由として、DE がエントリポイントに到達したことを意味します `CANSTOP_ENTRYPOINT` `CANSTOP_STEPIN` 。つまり、de が関数にステップインされたことを意味します。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)
- [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
