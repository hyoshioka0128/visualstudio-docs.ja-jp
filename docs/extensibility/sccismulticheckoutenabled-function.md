---
description: この関数は、ソース管理プラグインがファイルに対して複数のチェックアウトを許可しているかどうかを確認します。
title: SccIsMultiCheckoutEnabled 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 648b68f1575e31e81b6f12ca09abcb8e7305a985
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220561"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 関数
この関数は、ソース管理プラグインがファイルに対して複数のチェックアウトを許可しているかどうかを確認します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>パラメーター
 pContext

からソース管理プラグインのコンテキスト構造。

 pbMultiCheckout

入出力このプロジェクトに対して複数のチェックアウトを有効にするかどうかを指定します (0 以外の場合は複数のチェックアウトがサポートされます)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|チェックに成功しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 IDE は2つのチェックを行い、複数のユーザーが同時にファイルをチェックアウトできるかどうかを判断します。 まず、ソース管理システムが複数のチェックアウトをサポートしている必要があります。 ソース管理プラグインは、を指定することにより、初期化中にこの機能を指定でき `SCC_CAP_MULTICHECKOUT` ます。 その後、2番目のチェックとして、IDE はこの関数を呼び出して、現在のプロジェクトが複数のチェックアウトをサポートしているかどうかを判断します。 選択したプロジェクトで複数のチェックアウトがサポートされている場合、プラグインは成功コードを返し、 `pbMultiCheckout` を0以外 ( `TRUE` ) またはに設定し `FALSE` ます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
