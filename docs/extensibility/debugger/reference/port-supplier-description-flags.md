---
description: ポートサプライヤーに関する取得可能なメタデータを定義します。
title: PORT_SUPPLIER_DESCRIPTION_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- PORT_SUPPLIER_DESCRIPTION_FLAGS enumeration
ms.assetid: 5acee0ee-3a20-41c9-a7dc-0dadae6a5ba5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 09c3cb532b7fa9c496ad217c1f5ecacbbf2b8c5c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086314"
---
# <a name="port_supplier_description_flags"></a>PORT_SUPPLIER_DESCRIPTION_FLAGS

ポートサプライヤーに関する取得可能なメタデータを定義します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_PORT_SUPPLIER_DESCRIPTION_FLAGS
{
    PSDFLAG_SHOW_WARNING_ICON = 0x1
};
typedef DWORD PORT_SUPPLIER_DESCRIPTION_FLAGS;
```

```csharp
public enum enum_PORT_SUPPLIER_DESCRIPTION_FLAGS
{
    PSDFLAG_SHOW_WARNING_ICON = 0x1
};
```

## <a name="fields"></a>フィールド

`PSDFLAG_SHOW_WARNING_ICON`\
この設定を選択すると、UI に警告アイコンが表示されます。

## <a name="remarks"></a>注釈

この列挙体は、 [Getdescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md) メソッドによって返されます。

## <a name="requirements"></a>要件

ヘッダー: Msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目

- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)
