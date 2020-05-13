---
title: 表示情報 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayKind enumeration
ms.assetid: 940968c5-6065-4bda-8ee6-c31597db4d71
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f7634ae3ee03b7e577f0621ffc263e4d45bfe194
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737250"
---
# <a name="displaykind"></a>DisplayKind
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトから取得し、ユーザーに表示する情報の種類を表す有効な値を列挙します。

## <a name="syntax"></a>構文

```cpp
enum enum_DisplayKind
{
    DisplayKind_Value = 0x1,
    DisplayKind_Name = 0x2,
    DisplayKind_Type = 0x3,
};
typedef DWORD DisplayKind;
```

```csharp
public enum enum_DisplayKind
{
    DisplayKind_Value = 0x1,
    DisplayKind_Name = 0x2,
    DisplayKind_Type = 0x3,
};
```

## <a name="fields"></a>フィールド
`DisplayKind_Value`\
フィールドの値。

`DisplayKind_Name`\
フィールドの名前。

`DisplayKind_Type`\
フィールドの種類です。

## <a name="requirements"></a>必要条件
ヘッダー: Ee.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)
