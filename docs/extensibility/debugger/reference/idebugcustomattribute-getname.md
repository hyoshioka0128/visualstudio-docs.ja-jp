---
description: カスタム属性の名前を取得します。
title: 'IDebugCustomAttribute:: GetName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetName
helpviewer_keywords:
- IDebugCustomAttribute::GetName
ms.assetid: ba509cc5-5816-4925-a094-4c72d88c360c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7be47a763d4809d6e62b65660c39187d2d130065
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088069"
---
# <a name="idebugcustomattributegetname"></a>IDebugCustomAttribute::GetName
カスタム属性の名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName( 
   BSTR* bstrName
);
```

```csharp
int GetName(
   out string bstrName
);
```

## <a name="parameters"></a>パラメーター
`bstrName`\
入出力カスタム属性の名前を含む文字列を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドによって返されるという名前のは、属性の宣言に使用されるクラスの名前に対応します。 これは、カスタム属性クラス自体の名前に完全に対応しているとは限りません。 C# では、宣言で使用されている場合、"Attribute" サフィックスをカスタム属性名から削除することができます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
