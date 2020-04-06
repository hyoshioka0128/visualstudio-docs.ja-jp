---
title: オブジェクト2::IsUserデータ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::IsUserData
helpviewer_keywords:
- IDebugObject2::IsUserData method
ms.assetid: 6ffa0d0e-f742-496d-acc7-db74c248bc45
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce4a7035ac3786f0cc1644e2ebbb0c142167e2b0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726093"
---
# <a name="idebugobject2isuserdata"></a>IDebugObject2::IsUserData
オブジェクトがユーザー データを表すかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsUserData(
   BOOL* pfUser
);
```

```csharp
int IsUserData(
   out int pfUser
);
```

## <a name="parameters"></a>パラメーター
`pfUser`\
[アウト]オブジェクトがユーザー`TRUE`データを表す場合は、0 以外 ( ) を返します。ゼロ`FALSE`( ) が含まれていない場合。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ユーザー データは、JustMyCode として指定されたモジュールの一部であるオブジェクトです (モジュールをユーザー コードとしてマークし、スタック トレースに表示するユーザーが構成可能なオプション)。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
