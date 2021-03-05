---
description: スタックフレームの説明を取得します。
title: 'IDebugStackFrame2:: GetInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetInfo
helpviewer_keywords:
- IDebugStackFrame2::GetInfo
ms.assetid: 19c6870b-b94e-453c-bf19-82ce95b79d26
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3af7aafe43c0d7916a3fc11b855d5512f50a1d5f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168622"
---
# <a name="idebugstackframe2getinfo"></a>IDebugStackFrame2::GetInfo
スタックフレームの説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetInfo ( 
   FRAMEINFO_FLAGS dwFieldSpec,
   UINT            nRadix,
   FRAMEINFO*      pFrameInfo
);
```

```csharp
int GetInfo ( 
   enum_FRAMEINFO_FLAGS dwFieldSpec,
   uint                 nRadix,
   FRAMEINFO[]          pFrameInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFieldSpec`\
からパラメーターのどのフィールドを入力するかを指定する、 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md) 列挙のフラグの組み合わせ `pFrameInfo` 。

`nRadix`\
から数値情報の書式設定に使用される基数。

`pFrameInfo`\
入出力スタックフレームの説明と共に入力される [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
