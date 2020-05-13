---
title: PROCESS_INFO_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f81709e7146bbdef13daa3564bb784fd9c08d58e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714014"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
プロセスで取得する情報の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PROCESS_INFO_FIELDS { 
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
public enum enum_PROCESS_INFO_FIELDS { 
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
 PROCESS_INFO構造体のフィールド`bstrFileName`を初期化/[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)使用します。

 `PIF_BASE_NAME`\
 構造体のフィールドを`bstrBaseName`初期化/使用`PROCESS_INFO`します。

 `PIF_TITLE`\
 構造体のフィールドを`bstrTitle`初期化/使用`PROCESS_INFO`します。

 `PIF_PROCESS_ID`\
 構造体のフィールドを`ProcessId`初期化/使用`PROCESS_INFO`します。

 `PIF_SESSION_ID`\
 構造体のフィールドを`dwSessionId`初期化/使用`PROCESS_INFO`します。

 `PIF_ATTACHED_SESSION_NAME`\
 構造体のフィールドを`bstrAttachedSessionName`初期化/使用`PROCESS_INFO`します。

 `PIF_CREATION_TIME`\
 構造体のフィールドを`CreationTime`初期化/使用`PROCESS_INFO`します。

 `PIF_FLAGS`\
 構造体のフィールドを`Flags`初期化/使用`PROCESS_INFO`します。

 `PIF_ALL`\
 すべてのフィールドに入力します。

## <a name="remarks"></a>Remarks
 [初期化するPROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)構造体のフィールドを示すために[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)メソッドに渡されます。

 また、使用`Fields`および有効な`PROCESS_INFO`フィールドを示すために、構造体のフィールドで使用されます。

 これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
