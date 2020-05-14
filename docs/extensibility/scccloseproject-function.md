---
title: プロジェクト関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCloseProject
helpviewer_keywords:
- SccCloseProject function
ms.assetid: 259c2069-d349-4814-810f-1c3151b7fb84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 71df385bc0cf42c2437abfd117c2f84bda5b5432
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701046"
---
# <a name="scccloseproject-function"></a>関数を閉じる
この関数は、特定のセッションの終了をマークしてプロジェクトを閉じます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCloseProject (
   LPVOID pvContext
);
```

### <a name="parameters"></a>パラメーター
 pvContext ソース管理プラグインのコンテキスト構造。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトは正常に終了しました。|
|SCC_E_PROJNOTOPEN|現在開いているプロジェクトはありません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 [この](../extensibility/sccopenproject-function.md)関数の前に常に呼び出されます。 この関数の呼び出しの後に`SccOpenProject`、関数または[SccUninitialize](../extensibility/sccuninitialize-function.md)のいずれかの呼び出しが行われ、ソース管理システムへの接続が完全に終了します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
