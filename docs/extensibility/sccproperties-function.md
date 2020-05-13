---
title: SccProperties 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf2dd87efbb50346093144db6e069eea30138e37
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700504"
---
# <a name="sccproperties-function"></a>SccProperties 関数
この関数は、ファイルまたはプロジェクトのソース管理プロパティを表示します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccProperties (
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ファイル名

[in]ファイルまたはプロジェクトの完全修飾パス名。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|プロパティが正常に表示されました。|
|SCC_I_RELOADFILE|バージョン管理システムによってファイルプロパティが変更されているので、IDE はこのファイルを再ロードする必要があります。|
|SCC_E_PROJNOTOPEN|指定されたプロジェクトはソース管理で開かれていない。|
|SCC_E_NOTAUTHORIZED|ユーザーは、このファイルまたはプロジェクトのプロパティを表示する権限がありません。|
|SCC_E_FILENOTCONTROLLED|指定されたファイルまたはプロジェクトはソース管理下にありません。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不明または一般的なエラーが発生しました。|

## <a name="remarks"></a>Remarks
 ソース管理プラグインは、プロパティを独自のダイアログ ボックスに表示します。

 プロパティは、ソース管理プラグインによって定義され、プラグインによって異なる場合があります。 プラグインによってユーザーがファイルのソース管理プロパティを変更できる場合は、このファイルまたはプロジェクトの再`SCC_I_RELOAD`読み込みが必要であることを IDE に通知する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
