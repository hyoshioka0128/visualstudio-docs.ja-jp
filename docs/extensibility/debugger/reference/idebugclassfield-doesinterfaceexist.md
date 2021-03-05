---
description: クラスで特定のインターフェイスが定義されているかどうかを判断します。
title: IDebugClassField::D oesInterfaceExist |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4248b653f5eea43a91d0c78a593431d53f5e68b8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173469"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
クラスで特定のインターフェイスが定義されているかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT DoesInterfaceExist( 
   LPCOLESTR pszInterfaceName
);
```

```csharp
int DoesInterfaceExist(
   [In] string pszInterfaceName
);
```

## <a name="parameters"></a>パラメーター
`pszInterfaceName`\
から検索するインターフェイス名を格納している文字列。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返し、インターフェイスが存在しない場合は S_FALSE を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、すべてのインターフェイスの列挙体を取得し、一致するインターフェイスのリストを検索します。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
