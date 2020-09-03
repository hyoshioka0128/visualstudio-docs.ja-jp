---
title: IDebugProperty3::D estroyObjectID |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721202"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
このプロパティに関連付けられている一意の ID を破棄します。これは、呼び出し元が他のすべてのプロパティから一意にこのプロパティを識別しないことを示します。

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
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 デバッグエンジンがプロパティの一意の Id をサポートする必要がない場合 (既に内部的に一意に追跡しているため)、このメソッドに対して単にを返すことができ `E_NOTIMPL` ます。

 呼び出し元が、このプロパティが他のすべてのプロパティで一意に識別されるようにする場合は、 [Createobjectid](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md) メソッドを呼び出すことで一意の id が作成されます。

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
