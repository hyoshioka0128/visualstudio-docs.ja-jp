---
title: 3::DエストロイオブジェクトID |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::DestroyObjectID
helpviewer_keywords:
- IDebugProperty3::DestroyObjectID
ms.assetid: bd08f356-cc67-4717-98c9-c3d00cad2040
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f465bc06712c5032c6e90288ebd02406de4f2330
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721202"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
このプロパティに関連付けられた一意の ID を破棄し、呼び出し元が他のすべてのプロパティからこのプロパティを一意に識別することを気にしなくなったことを示します。

## <a name="syntax"></a>構文

```cpp
HRESULT DestroyObjectID(
   void
);
```

```csharp
int DestroyObjectID();
```

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 デバッグ エンジンがプロパティの一意の ID をサポートする必要がない場合 (既に内部的に一意に追跡しているため)、このメソッド`E_NOTIMPL`に対して単純に返すことができます。

 呼び出し元がこのプロパティが他のすべてのプロパティ間で一意に識別されることを確認する場合は[、CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)メソッドの呼び出しで一意の ID が作成されます。

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
