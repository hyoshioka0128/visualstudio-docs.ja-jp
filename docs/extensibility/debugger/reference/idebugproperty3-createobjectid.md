---
title: プロパティ 3::オブジェクト ID を作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d3993d674f029260dbe32d16c576cb239ff8d6d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721176"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
このプロパティの一意の ID を作成して、他のすべてのプロパティ間で一意であることを確認します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateObjectID(
   void
);
```

```csharp
int CreateObjectID();
```

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、セッションデバッグマネージャーが、このプロパティが他のすべてのプロパティの間で一意に識別されることを確認する場合に呼び出されます。 デバッグ エンジン (DE) は、そのデバッグ エンジンが処理するプロパティが既に一意に識別されていない限り、このメソッドをサポートします。 DE がこのメソッドをサポートしていない場合は、`E_NOTIMPL`を返します。

 で`CreateObjectID`作成された一意の ID は[、DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)メソッドが呼び出されると破棄されます。これはまた、このプロパティを一意に識別する必要性の終了を示します。

> [!NOTE]
> この一意の ID を取得するメソッドはありません。 `CreateObjectID`

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
