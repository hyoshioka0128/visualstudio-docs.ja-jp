---
title: SccisMulti チェックアウト有効関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e91eb566a820f4fe11ceb629643e1815dcb87a8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700580"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 関数
この関数は、ソース管理プラグインがファイルに対して複数のチェックアウトを許可するかどうかをチェックします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグインのコンテキスト構造。

 数十分なチェックアウト

[アウト]このプロジェクトに対して複数のチェックアウトが有効になっているかどうかを指定します (0 以外の場合は、複数のチェックアウトがサポートされます)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|チェックは成功しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 IDE では、複数のユーザーがファイルを同時にチェックアウトできるかどうかを確認するために 2 つのチェックが行われます。 まず、ソース管理システムは、複数のチェックアウトをサポートする必要があります。 ソース管理プラグインは、`SCC_CAP_MULTICHECKOUT`を指定することにより、初期化中にこの機能を指定できます。 その後、2 番目のチェックとして、IDE はこの関数を呼び出して、現在のプロジェクトが複数のチェックアウトをサポートしているかどうかを判断します。 選択したプロジェクトで複数のチェックアウトがサポートされている場合、プラグインは成功コードを返し、ゼロ以外`pbMultiCheckout`の (`TRUE`)`FALSE`または に設定します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
