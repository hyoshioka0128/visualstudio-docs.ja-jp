---
description: この関数は、プロジェクトを閉じて、特定のセッションの終了をマークします。
title: SccCloseProject 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCloseProject
helpviewer_keywords:
- SccCloseProject function
ms.assetid: 259c2069-d349-4814-810f-1c3151b7fb84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 05dbf0552242bdc1a21ec6dd81a592711f50f391
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085638"
---
# <a name="scccloseproject-function"></a>SccCloseProject 関数
この関数は、プロジェクトを閉じて、特定のセッションの終了をマークします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCloseProject (
   LPVOID pvContext
);
```

### <a name="parameters"></a>パラメーター
 pvContext ソース管理プラグインのコンテキスト構造。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトは正常に終了しました。|
|SCC_E_PROJNOTOPEN|現在開いているプロジェクトはありません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>注釈
 [Sccopenproject](../extensibility/sccopenproject-function.md)は、この関数の前に常に呼び出されます。 その後、この関数の呼び出しの後に、 `SccOpenProject` 関数または [Sccuninitialize](../extensibility/sccuninitialize-function.md)解除の呼び出しが行われます。これにより、ソース管理システムへの接続が完全に終了します。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
