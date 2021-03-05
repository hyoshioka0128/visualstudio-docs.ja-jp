---
description: 言語およびベンダー識別子を指定して、使用可能な式エバリュエーターを列挙します。
title: 'IDebugSettingsCallback2:: EnumEEs |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::EnumEEs
ms.assetid: 9f884c49-426f-461b-b547-9d909486e73f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6ccd154643ece5f9ec87ee0fdb063082e7d371d8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168804"
---
# <a name="idebugsettingscallback2enumees"></a>IDebugSettingsCallback2::EnumEEs
言語およびベンダー識別子を指定して、使用可能な式エバリュエーターを列挙します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumEEs(
   DWORD  celtBuffer,
   GUID*  rgguidLang,
   GUID*  rgguidVendor,
   DWORD* pceltEEs
);
```

```csharp
public int EnumEEs(
   uint       celtBuffer,
   ref Guid   rgguidLang,
   ref Guid   rgguidVendor,
   ref uint[] pceltEEs
);
```

## <a name="parameters"></a>パラメーター
`celtBuffer`\
からバッファー内の要素の数 `pceltEEs` 。

`rgguidLang`\
[入力、出力]プログラミング言語の一意の識別子。

`rgguidVendor`\
[入力、出力]ベンダーの一意識別子。

`pceltEEs`\
[入力、出力]式エバリュエーターの配列。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
