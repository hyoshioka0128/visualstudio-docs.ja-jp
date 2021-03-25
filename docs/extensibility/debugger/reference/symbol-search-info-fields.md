---
description: 取得するシンボル情報の種類を指定します。
title: SYMBOL_SEARCH_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SYMBOL_SEARCH_INFO_FIELDS
helpviewer_keywords:
- SYMBOL_SEARCH_INFO_FIELDS enumeration
ms.assetid: bce35af0-722d-46d4-afa6-eaae598c51ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 893cc51767be8977c6c298b56ffffee60c93bbbc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070909"
---
# <a name="symbol_search_info_fields"></a>SYMBOL_SEARCH_INFO_FIELDS
取得するシンボル情報の種類を指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_SYMBOL_SEARCH_INFO_FIELDS
{
   SSIF_NONE                = 0x00000000,
   SSIF_VERBOSE_SEARCH_INFO = 0x00000001
};
typedef DWORD SYMBOL_SEARCH_INFO_FIELDS;
```

```csharp
public enum enum_SYMBOL_SEARCH_INFO_FIELDS
{
   SSIF_NONE                = 0x00000000,
   SSIF_VERBOSE_SEARCH_INFO = 0x00000001
};

```

## <a name="fields"></a>フィールド
 `SSIF_NONE`\
 フラグがないことを示します。

 `SSIF_VERBOSE_SEARCH_INFO`\
 シンボルを検索するために使用されるすべての検索パスを返します

## <a name="remarks"></a>注釈
 これらのフラグは、返される情報の量を決定するために、 [Getシンボル情報](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md) メソッドにパラメーターとして渡されます。

> [!NOTE]
> 現時点では、のみ `SSIF_VERBOSE_SEARCH_INFO` がサポートされており、のパラメーターとして指定する必要があり `dwFlags` `IDebugModule3::GetSymbolInfo` ます。 その他の値はすべてエラーを返します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)
