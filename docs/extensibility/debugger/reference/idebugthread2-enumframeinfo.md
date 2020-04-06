---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::EnumFrameInfo
helpviewer_keywords:
- IDebugThread2::EnumFrameInfo
ms.assetid: 17914a71-10ea-4b6f-8982-e364f87dca53
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8bd3c6d46a577930cc7a2b87c85cd82a55f8cf66
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718842"
---
# <a name="idebugthread2enumframeinfo"></a>IDebugThread2::EnumFrameInfo
このスレッドのスタック フレームの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumFrameInfo ( 
   FRAMEINFO_FLAGS        dwFieldSpec,
   UINT                   nRadix,
   IEnumDebugFrameInfo2** ppEnum
);
```

```csharp
int EnumFrameInfo ( 
   enum_FRAMEINFO_FLAGS     dwFieldSpec,
   uint                     nRadix,
   out IEnumDebugFrameInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFieldSpec`\
[in][frameINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体のどのフィールドに入力するかを指定する[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)列挙体のフラグの組み合わせ。関数名`FIF_FUNCNAME_FORMAT`を単一の文字列にフォーマットするフラグを指定します。

`nRadix`\
[in]列挙子の数値情報の書式設定に使用される基数。

`ppEnum`\
[アウト]スタック[フレーム](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)を記述する[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体の一覧を含むオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 スレッドのフレームは順番に列挙され、現在のフレームが最初に列挙され、最も古いフレームが最後に列挙されます。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
