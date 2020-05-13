---
title: プロパティ 2::セットバリューアスストリング |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 112ded163f38b93e9918387d8ca6beafb8282647
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721240"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
指定された文字列からプロパティの値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValueAsString ( 
   LPCOLESTR pszValue,
   UINT      nRadix,
   DWORD     dwTimeout
);
```

```csharp
int SetValueAsString ( 
   string pszValue,
   uint   nRadix,
   uint   dwTimeout
);
```

## <a name="parameters"></a>パラメーター
`pszValue`\
[in]設定する値を含む文字列。

`nRadix`\
[in]数値情報の解釈に使用する基数。 これは、基数を自動的に決定する場合に 0 を指定できます。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間をミリ秒単位で指定します。 無期限`INFINITE`に待機するために使用します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 次の表に、その他の値を示します。

|[値]|説明|
|-----------|-----------------|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|文字列をプロパティ値に変換できなかったか、プロパティ値を設定できませんでした。|
|`E_SETVALUE_VALUE_IS_READONLY`|このプロパティは読み取り専用です。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
