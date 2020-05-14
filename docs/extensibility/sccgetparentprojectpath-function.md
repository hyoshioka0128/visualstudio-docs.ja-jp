---
title: 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetParentProjectPath
helpviewer_keywords:
- SccGetParentProjectPath function
ms.assetid: 62a71579-36b3-48b9-a1c8-04ab100efa08
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f258558207f86ff76746d18aa432fe4c5850290
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700710"
---
# <a name="sccgetparentprojectpath-function"></a>関数
この関数は、指定されたプロジェクトの親プロジェクト パスを決定します。 この関数は、ユーザーが Visual Studio プロジェクトをソース管理に追加するときに呼び出されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetParentProjectPath(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpProjPath,
   LPSTR  lpAuxProjPath,
   LPSTR  lpParentProjPath
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ユーザー数を指定します。

[イン、アウト]ユーザー名 (null 終端文字を含むSCC_USER_SIZEまで)。

 パス

[in]プロジェクトパスを識別する文字列 (null 終端文字を含む、SCC_PRJPATH_SIZEまで)。

 プロウプロイパス

[イン、アウト]プロジェクトを識別する補助文字列 (null 終端文字を含むSCC_PRJPATH_SIZEまで)。

 パス

[イン、アウト]親プロジェクトパスを識別する出力文字列 (null 終端文字を含む、SCC_PRJPATH_SIZEまで)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|親プロジェクトパスが正常に取得されました。|
|SCC_E_INITIALIZEFAILED|プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーはソース管理プラグインにログインできませんでした。|
|SCC_E_UNKNOWNPROJECT|プロジェクトはソース管理プラグインに対して不明です。|
|SCC_E_INVALIDFILEPATH|無効なファイル パスまたは使用できないファイル パスです。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_PROJSYNTAXERR|プロジェクト構文が無効です。|
|SCC_E_CONNECTIONFAILURE|ストア接続の問題。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 この関数は、成功または失敗のコードを返し、成功した場合は`lpParentProjPath`、指定されたプロジェクトへの完全なプロジェクト パスを変数に入力します。

 この関数は、既存のプロジェクトの親プロジェクト パスを返します。 ルート プロジェクトの場合、関数は渡されたプロジェクト パス (つまり、同じルート プロジェクト パス) を返します。 プロジェクト パスは、ソース管理プラグインにのみ意味のある文字列です。

 IDE は、`lpUser`および`lpAuxProjPath`パラメーターの変更も受け入れる準備ができています。 IDE は、これらの文字列を保持し、ユーザーが将来このプロジェクトを開いたときに[、SccOpenProject](../extensibility/sccopenproject-function.md)に渡します。 したがって、これらの文字列は、ソース管理プラグインがプロジェクトに関連付ける必要がある情報を追跡する方法を提供します。

 この関数は、プロジェクトを選択するようにユーザーに求めないことを除いて[、SccGetProjPath](../extensibility/sccgetprojpath-function.md)に似ています。 また、新しいプロジェクトを作成することは決してありませんが、既存のプロジェクトでのみ機能します。

 When`SccGetParentProjectPath`が呼`lpProjPath`び`lpAuxProjPath`出され、空ではなく、有効なプロジェクトに対応します。 これらの文字列は、通常、関数に対する以前の呼び`SccGetProjPath`出しから IDE によって受け取られます。

 引数`lpUser`はユーザー名です。 IDE は、以前に関数から受け取ったユーザー名と同`SccGetProjPath`じ名前を渡し、ソース管理プラグインは、この名前をデフォルトとして使用する必要があります。 ユーザーがプラグインと既にオープンな接続を持っている場合、プラグインは、関数がサイレントで動作することを確認するプロンプトを除去しようとする必要があります。 ただし、ログインが失敗した場合、プラグインはユーザーにログインを求め、有効なログインを受け取ったら、その名前をに戻`lpUser`す必要があります。 プラグインはこの文字列を変更する可能性があるため、IDE は常にサイズ (+1)`SCC_USER_LEN`のバッファを割り当てます。 文字列が変更された場合、新しい文字列は有効なログイン名でなければなりません(少なくとも古い文字列と同じくらい有効)。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateサブプロジェクトとSccGet親プロジェクトパスのテクニカル ノート
 Visual Studio では、ソース管理システム内の場所を選択するように求めるメッセージが表示される回数を最小限に抑えるために、ソリューションとプロジェクトをソース管理に追加する作業が簡略化されました。 ソース管理プラグインが新しい機能[、SccCreateSubProject](../extensibility/scccreatesubproject-function.md)と関数の両方をサポートしている場合、これらの変更は`SccGetParentProjectPath`Visual Studio によってアクティブになります。 ただし、次のレジストリ エントリを使用して、これらの変更を無効にし、以前の Visual Studio (ソース管理プラグイン API バージョン 1.1) の動作に戻すことができます。

 **[HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール]"ソリューション ルート フォルダー内ソース コントロール"=dword:00000001**

 このレジストリ エントリが存在しないか、または dword:0000000 に設定されている場合、Visual Studio は新`SccCreateSubProject`しい`SccGetParentProjectPath`関数を使用しようとします。

 レジストリ エントリが dword:0000001 に設定されている場合、Visual Studio はこれらの新しい関数を使用しようとせず、ソース管理に追加する操作は、以前のバージョンの Visual Studio と同じように機能します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
