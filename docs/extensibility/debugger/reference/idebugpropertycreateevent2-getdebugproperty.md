---
title: 'IDebugPropertyCreateEvent2:: GetDebugProperty |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2::GetDebugProperty
helpviewer_keywords:
- IDebugPropertyCreateEvent2::GetDebugProperty
ms.assetid: d7e43183-444c-4417-af19-82e28229f83a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c041a9dca28dfbd0b1138e45809143e87d0809db
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876070"
---
# <a name="idebugpropertycreateevent2getdebugproperty"></a>IDebugPropertyCreateEvent2::GetDebugProperty
新しいプロパティを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDebugProperty ( 
   IDebugProperty2** ppProperty
);
```

```csharp
int GetDebugProperty ( 
   out IDebugProperty2 ppProperty
);
```

## <a name="parameters"></a>パラメーター
`ppProperty`\
入出力新しいプロパティを表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
