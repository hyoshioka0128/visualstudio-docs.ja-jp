---
description: このスレッドのスタックフレームの一覧を取得します。
title: 'IDebugThread2:: Enumフレーム情報 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::EnumFrameInfo
helpviewer_keywords:
- IDebugThread2::EnumFrameInfo
ms.assetid: 17914a71-10ea-4b6f-8982-e364f87dca53
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c9ad740de00338596de622cbce1028768ddda638
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149341"
---
# <a name="idebugthread2enumframeinfo"></a>IDebugThread2::EnumFrameInfo
このスレッドのスタックフレームの一覧を取得します。

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
から[フレーム情報](../../../extensibility/debugger/reference/frameinfo.md)構造体のどのフィールドを入力するかを指定する、 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)列挙型のフラグの組み合わせ。`FIF_FUNCNAME_FORMAT`関数名を1つの文字列に書式設定するフラグを指定します。

`nRadix`\
から列挙子の数値情報の書式設定に使用される基数。

`ppEnum`\
入出力スタックフレームを説明するフレーム[情報](../../../extensibility/debugger/reference/frameinfo.md)構造体のリストを格納している[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 スレッドのフレームは順番に列挙され、現在のフレームが列挙され、最も古いフレームが最後に列挙されます。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
