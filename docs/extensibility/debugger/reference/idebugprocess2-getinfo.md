---
description: プロセスの説明を取得します。
title: 'IDebugProcess2:: GetInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetInfo
helpviewer_keywords:
- IDebugProcess2::GetInfo
ms.assetid: 46021dce-bb97-46c3-b0cc-e5b3b68acc35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6e6b8e0c14cee960d1991ae4f5a482f66e89465
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169211"
---
# <a name="idebugprocess2getinfo"></a>IDebugProcess2::GetInfo
プロセスの説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetInfo(
   PROCESS_INFO_FIELDS  Fields,
   PROCESS_INFO*        pProcessInfo
);
```

```csharp
int GetInfo(
   enum_PROCESS_INFO_FIELDS  Fields,
   PROCESS_INFO[]            pProcessInfo
);
```

## <a name="parameters"></a>パラメーター
`Fields`\
からパラメーターのどのフィールドを入力するかを指定する、 [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md) 列挙型の値の組み合わせ `pProcessInfo` 。

`pProcessInfo`\
入出力プロセスの説明が入力されている [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
