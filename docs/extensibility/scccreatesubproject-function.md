---
title: 関数を作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74354e05b16830f599dd706fbe48aadd75b11a18
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701036"
---
# <a name="scccreatesubproject-function"></a>関数
この関数は、引数で指定された既存の親プロジェクトの下に、指定された`lpParentProjPath`名前のサブプロジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCreateSubProject(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpParentProjPath,
   LPCSTR lpSubProjName,
   LPSTR  lpAuxProjPath,
   LPSTR  lpSubProjPath
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ユーザー数を指定します。

[イン、アウト]ユーザー名 (null ターミネータを含むSCC_USER_SIZEまで)。

 パス

[in]親プロジェクトのパスを識別する文字列 (null 終端文字を含むSCC_PRJPATH_SIZEまで)。

 名前を変更します。

[in]推奨されるサブプロジェクト名 (null 終端文字を含むSCC_PRJPATH_SIZEまで)。

 プロウプロイパス

[イン、アウト]プロジェクトを識別する補助文字列 (null 終端文字を含むSCC_PRJPATH_SIZEまで)。

 パス

[イン、アウト]サブプロジェクトのパスを示す出力文字列 (null 終端文字を含むSCC_PRJPATH_SIZEまで)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|サブプロジェクトが正常に作成されました。|
|SCC_E_INITIALIZEFAILED|親プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーはソース管理システムにログインできませんでした。|
|SCC_E_COULDNOTCREATEPROJECT|サブプロジェクトを作成できません。|
|SCC_E_PROJSYNTAXERR|プロジェクト構文が無効です。|
|SCC_E_UNKNOWNPROJECT|親プロジェクトがソース管理プラグインに対して不明です。|
|SCC_E_INVALIDFILEPATH|無効なファイル パスまたは使用できないファイル パスです。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_CONNECTIONFAILURE|ソース管理プラグイン接続の問題が発生しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 名前のサブプロジェクトが既に存在する場合、関数は、たとえば"_\<number>" を追加して、既定の名前を変更して一意の名前を作成できます。 呼び出し元は、 、`lpUser``lpSubProjPath`および`lpAuxProjPath`への変更を受け入れる準備をしておく必要があります。 `lpSubProjPath`引数と`lpAuxProjPath`引数は[、SccOpenProject](../extensibility/sccopenproject-function.md)への呼び出しで使用されます。 返された場合、呼び出し元によって変更しないでください。 これらの文字列は、ソース管理プラグインがプロジェクトに関連付ける必要がある情報を追跡する方法を提供します。 プラグインは表示に適さない書式付き文字列を使用できるため、返された場合に、呼び出し元の IDE ではこれらの 2 つのパラメーターは表示されません。 関数は成功または失敗のコードを返し、成功した場合は、新`lpSubProjPath`しいプロジェクトへの完全なプロジェクト パスを変数に入力します。

 この関数は[SccGetProjPath](../extensibility/sccgetprojpath-function.md)に似ていますが、ユーザーに選択を求めるのではなく、プロジェクトをサイレントで作成する点が異なります。 関数が`SccCreateSubProject`呼び出され`lpParentProjName``lpAuxProjPath`、空ではなく、有効なプロジェクトに対応する場合。 これらの文字列は、通常、関数または`SccGetProjPath`[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)への以前の呼び出しから IDE によって受信されます。

 引数`lpUser`はユーザー名です。 IDE は、以前に から`SccGetProjPath`受け取ったユーザー名と同じ名前を渡し、ソース管理プラグインはデフォルト名としてこの名前を使用する必要があります。 ユーザーがプラグインと既にオープンな接続を持っている場合、プラグインは、関数がサイレントで動作することを確認するプロンプトを除去しようとする必要があります。 ただし、ログインが失敗した場合、プラグインはユーザーにログインを求め、有効なログインを受け取ったら、その名前をに戻`lpUser`す必要があります。 プラグインはこの文字列を変更する可能性があるため、IDE は常にサイズのバッファー (SCC_USER_LEN+1 または SCC_USER_SIZE (null ターミネータ用のスペースを含む) を割り当てます。 文字列が変更された場合、新しい文字列は有効なログイン名でなければなりません(少なくとも古い文字列と同じくらい有効)。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateサブプロジェクトとSccGet親プロジェクトパスのテクニカル ノート
 Visual Studio では、ソース管理システム内の場所を選択するように求めるメッセージが表示される回数を最小限に抑えるために、ソリューションとプロジェクトをソース管理に追加する作業が簡略化されました。 これらの変更は、ソース管理プラグインが両方の新機能をサポートしている場合、Visual `SccCreateSubProject` Studio によってアクティブ`SccGetParentProjectPath`化されます。 ただし、次のレジストリ エントリを使用して、これらの変更を無効にし、以前の Visual Studio (ソース管理プラグイン API バージョン 1.1) の動作に戻すことができます。

 **[HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール]"ソリューション ルート フォルダー内ソース コントロール"=dword:00000001**

 このレジストリ エントリが存在しないか、または dword:0000000 に設定されている場合、Visual Studio は新`SccCreateSubProject`しい`SccGetParentProjectPath`関数を使用しようとします。

 レジストリ エントリが dword:0000001 に設定されている場合、Visual Studio はこれらの新しい関数を使用しようとせず、ソース管理に追加する操作は、以前のバージョンの Visual Studio と同じように機能します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
