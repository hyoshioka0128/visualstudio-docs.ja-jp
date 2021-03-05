---
description: この関数は、前のチェックアウト操作を元に戻します。これにより、選択したファイルの内容がチェックアウト前の状態に復元されます。
title: SccUncheckout 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 33e0c4904a92d71e000d8c911d551eb8d0aab621
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221354"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 関数
この関数は、前のチェックアウト操作を元に戻します。これにより、選択したファイルの内容がチェックアウト前の状態に復元されます。 チェックアウト後にファイルに加えられたすべての変更は失われます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccUncheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

から配列に指定されたファイルの数 `lpFileNames` 。

 lpFileNames 名

からチェックアウトを元に戻すファイルの完全修飾ローカルパス名の配列。

 限ら

からコマンドフラグ (使用されていません)。

 pvOptions

からソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|チェックアウトが正常に取り消されました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソースコード管理されていません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 チェックアウトを元に戻す操作に失敗しました。|
|SCC_E_NOTCHECKEDOUT|ユーザーにはファイルがチェックアウトされていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理から開かれていません。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|

## <a name="remarks"></a>解説
 この操作の後、 `SCC_STATUS_CHECKEDOUT` `SCC_STATUS_MODIFIED` undo チェックアウトが実行されたファイルに対して、フラグとフラグの両方がクリアされます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
