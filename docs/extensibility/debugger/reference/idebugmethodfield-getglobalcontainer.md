---
title: 'IDebugMethodField:: GetGlobalContainer |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetGlobalContainer
helpviewer_keywords:
- IDebugMethodField::GetGlobalContainer method
ms.assetid: 041ac5aa-0b80-4310-b9ae-b88f8e7e0e5f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 37e3b26a265fe651216e46fa299bdd827416b8ce
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727126"
---
# <a name="idebugmethodfieldgetglobalcontainer"></a>IDebugMethodField::GetGlobalContainer
メソッドのグローバルコンテナーを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetGlobalContainer(
   IDebugClassField** ppClass
);
```

```csharp
int GetGlobalContainer(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>パラメーター
`ppClass`\
入出力このメソッドが定義されているモジュールを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 返される [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトは、モジュール全体を表し、人工のオブジェクトです。つまり、モジュール自体に実際のクラスはありませんが、オブジェクトで表すことができるの `IDebugClassField` で、モジュールのさまざまな要素を列挙して検出できます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
