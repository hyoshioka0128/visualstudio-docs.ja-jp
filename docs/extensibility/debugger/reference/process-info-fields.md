---
description: プロセスに対して取得する情報の種類を指定します。
title: PROCESS_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d1f779352ce6b1217cd8af1e87988cb165b2dddc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079632"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
プロセスに対して取得する情報の種類を指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
typedef DWORD PROCESS_INFO_FIELDS;
```

```csharp
public enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
```

## <a name="fields"></a>フィールド
 `PIF_FILE_NAME`\
 `bstrFileName` [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)構造体のフィールドを初期化/使用します。

 `PIF_BASE_NAME`\
 構造体のフィールドを初期化/使用し `bstrBaseName` `PROCESS_INFO` ます。

 `PIF_TITLE`\
 構造体のフィールドを初期化/使用し `bstrTitle` `PROCESS_INFO` ます。

 `PIF_PROCESS_ID`\
 構造体のフィールドを初期化/使用し `ProcessId` `PROCESS_INFO` ます。

 `PIF_SESSION_ID`\
 構造体のフィールドを初期化/使用し `dwSessionId` `PROCESS_INFO` ます。

 `PIF_ATTACHED_SESSION_NAME`\
 構造体のフィールドを初期化/使用し `bstrAttachedSessionName` `PROCESS_INFO` ます。

 `PIF_CREATION_TIME`\
 構造体のフィールドを初期化/使用し `CreationTime` `PROCESS_INFO` ます。

 `PIF_FLAGS`\
 構造体のフィールドを初期化/使用し `Flags` `PROCESS_INFO` ます。

 `PIF_ALL`\
 すべてのフィールドを入力します。

## <a name="remarks"></a>注釈
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)構造体のどのフィールドを初期化するかを示すために[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)メソッドに渡されます。

 また `Fields` 、構造体のフィールドで、使用され `PROCESS_INFO` ているフィールドと有効なフィールドを示すためにも使用されます。

 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
