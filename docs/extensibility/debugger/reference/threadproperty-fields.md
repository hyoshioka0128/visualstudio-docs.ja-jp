---
description: スレッドに関する情報を取得するかどうかを指定します。
title: THREADPROPERTY_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 698c803304cf5efd3375b6d49e4dedbc4622f4c1
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221835"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
スレッドに関する情報を取得するかどうかを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_THREADPROPERTY_FIELDS { 
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
public enum enum_THREADPROPERTY_FIELDS { 
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
 `dwThreadId` [Threadproperties](../../../extensibility/debugger/reference/threadproperties.md)構造体のフィールドを初期化/使用します。

 `TPF_SUSPENDCOUNT`\
 `dwSuspendCount`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。

 `TPF_STATE`\
 `dwThreadState`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。

 `TPF_PRIORITY`\
 `bstrPriority`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。

 `TPF_NAME`\
 `bstrName`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。

 `TPF_LOCATION`\
 `bstrLocation`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。

 `TPF_ALLFIELDS`\
 すべてのフィールドを指定します。

## <a name="remarks"></a>解説
 これらの値は、引数として [Getthreadproperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) メソッドに渡さ [れ、どの](../../../extensibility/debugger/reference/threadproperties.md) フィールドを初期化するかを示します。

 これらの値は `dwFields` 、使用される `THREADPROPERTIES` フィールドと有効なフィールドを示すために、構造体のメンバーでも使用されます。

 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
