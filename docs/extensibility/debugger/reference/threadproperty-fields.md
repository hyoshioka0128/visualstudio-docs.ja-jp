---
title: THREADPROPERTY_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b31c43187d1136f7a194c42749c430de6cd064a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713396"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
取得するスレッドに関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
typedef DWORD THREADPROPERTY_FIELDS;
```

```csharp
public enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>フィールド
 `TPF_ID`\
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)構造体`dwThreadId`のフィールドを初期化/使用します。

 `TPF_SUSPENDCOUNT`\
 S 構造体の`dwSuspendCount`フィールドを初期化`THREADPROPERTIE`/使用します。

 `TPF_STATE`\
 S 構造体の`dwThreadState`フィールドを初期化`THREADPROPERTIE`/使用します。

 `TPF_PRIORITY`\
 S 構造体の`bstrPriority`フィールドを初期化`THREADPROPERTIE`/使用します。

 `TPF_NAME`\
 S 構造体の`bstrName`フィールドを初期化`THREADPROPERTIE`/使用します。

 `TPF_LOCATION`\
 S 構造体の`bstrLocation`フィールドを初期化`THREADPROPERTIE`/使用します。

 `TPF_ALLFIELDS`\
 すべてのフィールドを指定します。

## <a name="remarks"></a>Remarks
 これらの値は、初期化する[THREADPROPERTIES](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)構造体のフィールドを示すメソッドに引数[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)として渡されます。

 これらの値は、`dwFields``THREADPROPERTIES`構造体のメンバーで使用され、どのフィールドが使用され、有効かを示すためにも使用されます。

 これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
