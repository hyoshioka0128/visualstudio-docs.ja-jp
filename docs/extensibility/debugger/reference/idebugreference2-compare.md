---
description: ある参照と別の参照を比較します。
title: 'IDebugReference2:: Compare |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::Compare
helpviewer_keywords:
- IDebugReference2::Compare
ms.assetid: 3361c495-2673-4b7c-82e3-dee74e1fa58d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 017dfa60c1f854a36f1087bef87203f0b22ae4dc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083636"
---
# <a name="idebugreference2compare"></a>IDebugReference2::Compare
ある参照と別の参照を比較します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT Compare ( 
   REFERENCE_COMPARE dwCompare,
   IDebugReference2* pReference
);
```

```csharp
int Compare ( 
   enum_REFERENCE_COMPARE dwCompare,
   IDebugReference2       pReference
);
```

## <a name="parameters"></a>パラメーター
`dwCompare`\
から比較演算を指定する [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md) 列挙型の値 (等しい、未満、またはより大きいなど)。

`pReference`\
からと比較する参照を表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md)
