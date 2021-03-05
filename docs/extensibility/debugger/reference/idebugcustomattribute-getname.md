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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 313408639b0a93faef0c63c0add92dc1ca2e947b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163058"
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

## <a name="remarks"></a>解説
 このメソッドによって返されるという名前のは、属性の宣言に使用されるクラスの名前に対応します。 これは、カスタム属性クラス自体の名前に完全に対応しているとは限りません。 C# では、宣言で使用されている場合、"Attribute" サフィックスをカスタム属性名から削除することができます。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
