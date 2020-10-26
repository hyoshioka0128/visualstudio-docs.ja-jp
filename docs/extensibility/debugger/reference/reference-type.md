---
title: REFERENCE_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- REFERENCE_TYPE
helpviewer_keywords:
- REFERENCE_TYPE enumeration
ms.assetid: b1ffba10-eb9d-48ba-bf48-6d8b71d6f270
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29ce6ad17aa32b98fd28914c422a49bd8bcc14b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80713656"
---
# <a name="reference_type"></a>REFERENCE_TYPE
参照の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_REFERENCE_TYPE { 
   REF_TYPE_WEAK   = 0x0001,
   REF_TYPE_STRONG = 0x0002
};
typedef DWORD REFERENCE_TYPE;
```

```csharp
public enum enum_REFERENCE_TYPE { 
   REF_TYPE_WEAK   = 0x0001,
   REF_TYPE_STRONG = 0x0002
};
```

## <a name="fields"></a>フィールド
 `REF_TYPE_WEAK`\
 弱い参照を指定します。 をと組み合わせることはできません `REF_TYPE_STRONG` 。

 `REF_TYPE_STRONG`\
 強い参照を指定します。 をと組み合わせることはできません `REF_TYPE_WEAK` 。

## <a name="remarks"></a>注釈
 `dwRefType` [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体のメンバーとして使用されます。

 [SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)メソッドにパラメーターとして渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)
