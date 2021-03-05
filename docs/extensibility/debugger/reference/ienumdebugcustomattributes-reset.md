---
description: カスタム属性の列挙シーケンスを先頭にリセットします。
title: 'IEnumDebugCustomAttributes:: Reset |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::Reset
helpviewer_keywords:
- IEnumDebugCustomAttributes::Reset
ms.assetid: e0db6518-5a71-4adb-a407-4d2ac7a3e369
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d3393f2b87043345156337976ed12d10928572d2
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102226892"
---
# <a name="ienumdebugcustomattributesreset"></a>IEnumDebugCustomAttributes::Reset
列挙のシーケンスを最初にリセットします。

## <a name="syntax"></a>構文

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドが呼び出された後 [、次のメソッドを](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md) 呼び出すと、列挙体の最初の要素が返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md)
