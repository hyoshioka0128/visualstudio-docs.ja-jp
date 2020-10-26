---
title: IDebugPortPicker::D isplayPortPicker |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e0a02169b37bba804034990ed5d972f973244769
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80724893"
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

## <a name="see-also"></a>関連項目
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
