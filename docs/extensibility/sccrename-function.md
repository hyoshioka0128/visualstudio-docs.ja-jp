---
title: SccRename 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 88a917e43729b3049e488264c260f8455ab08fe4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700426"
---
# <a name="sccrename-function"></a>SccRename 関数
この関数は、ソース管理システム内のファイルの名前を変更します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccRename(
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName,
   LPCSTR lpNewName
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ファイル名

[in]名前を変更するファイルの完全修飾ファイル名。

 新しい名前を指定します。

[in]完全修飾の新しい名前。 ディレクトリパスが異なる場合、ファイルはサブディレクトリ間で移動します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|名前変更操作は正常に完了しました。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理下で開かれていない。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理下にありません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。|
|SCC_E_NOTAUTHORIZED|ユーザーには、この操作を完了する権限がありません。|
|SCC_E_COULDNOTCREATEPROJECT|名前の変更プロセスの一環としてプロジェクトを作成できませんでした。|
|SCC_E_OPNOTPERFORMED|操作は実行されませんでした。|
|SCC_E_NONSPECIFICERROR|未指定または一般的なエラーが発生しました。|

## <a name="remarks"></a>Remarks
 この関数を使用して、ファイルの名前を変更したり、ソース管理システム内の別の場所に移動したりできます。 ソース管理プラグインは、ディスク上のファイルにアクセスしようとしません。 ローカルファイルの名前を変更するのは IDE の責任です。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
