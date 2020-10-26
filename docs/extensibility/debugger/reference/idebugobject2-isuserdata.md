---
title: 'IDebugObject2:: IsUserData |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80726093"
---
# <a name="idebugobject2isuserdata"></a>IDebugObject2::IsUserData
オブジェクトがユーザーデータを表すかどうかを判断します。

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
入出力`TRUE`オブジェクトがユーザーデータを表している場合は0以外 () を返し、 `FALSE` そうでない場合はゼロ () を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 ユーザーデータとは、"ジャスト Mycode" として指定されたモジュールの一部である任意のオブジェクトです (ユーザーが構成可能なオプションで、モジュールをユーザーコードとしてマークし、スタックトレースに表示します)。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
