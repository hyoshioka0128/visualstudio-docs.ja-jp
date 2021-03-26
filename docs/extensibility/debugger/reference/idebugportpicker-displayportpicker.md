---
description: 指定されたダイアログボックスを表示し、ユーザーがポートを選択できるようにします。
title: IDebugPortPicker::D isplayPortPicker |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a49c1379d2bb3946f75eddd9d80bdccdb370d3ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072313"
---
# <a name="idebugportpickerdisplayportpicker"></a>IDebugPortPicker::DisplayPortPicker
指定されたダイアログボックスを表示し、ユーザーがポートを選択できるようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT DisplayPortPicker(
   HWND hwndParentDialog,
   BSTR* pbstrPortId
);
```

```csharp
public int DisplayPortPicker(
   int hwndParentDialog,
   out string pbstrPortId
);
```

## <a name="parameters"></a>パラメーター
`hwndParentDialog`\
から親ダイアログボックスのハンドル。

`pbstrPortId`\
入出力ポート識別子文字列。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 戻り値 `S_FALSE` (またはがに設定されたの戻り値) は、 `S_OK` `BSTR` `NULL` ユーザーが **[キャンセル]** をクリックしたことを示します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
