---
title: メソッドフィールド::ゲットグローバルコンテナ |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727126"
---
# <a name="idebugmethodfieldgetglobalcontainer"></a>IDebugMethodField::GetGlobalContainer
メソッドのグローバル コンテナーを取得します。

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
[アウト]このメソッドが定義されているモジュールを表す[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 返された[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)オブジェクトは、モジュール全体を表し、人工オブジェクトである、つまり、モジュール自体は実際のクラスを持たないが、`IDebugClassField`オブジェクトによって表すことができる、モジュールのさまざまな要素を列挙し、検出することができます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
