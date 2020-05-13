---
title: を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetExceptionObjectAndType
helpviewer_keywords:
- IDebugBinder3::GetExceptionObjectAndType method
ms.assetid: 2a313fe1-4ee1-4f01-af86-382d6c661a8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e25a0f7b4e1713a072359f1efdd962f36c50b774
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735750"
---
# <a name="idebugbinder3getexceptionobjectandtype"></a>IDebugBinder3::GetExceptionObjectAndType
このメソッドは、オブジェクトに関連付けられている例外を取得します (存在する場合)。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExceptionObjectAndType(
   IDebugObject** ppException,
   IDebugField**  ppField
);
```

```csharp
int GetExceptionObjectAndType(
   out IDebugObject ppException,
   out IDebugField  ppField
);
```

## <a name="parameters"></a>パラメーター
`ppException`\
[アウト]例外を表すオブジェクトを返します。

`ppField`\
[アウト]例外の原因となった特定のフィールドを表すオブジェクトを返します (NULL 値である可能性があります)。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

> [!NOTE]
> 例外があるかどうかを確認するには、 : が返す`ppException`値が null の場合、このオブジェクトに例外が関連付けられていないかどうかを確認します。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
