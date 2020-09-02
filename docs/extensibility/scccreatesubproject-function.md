---
title: SccCreateSubProject 関数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701036"
---
# <a name="scccreatesubproject-function"></a>SccCreateSubProject 関数
この関数は、引数で指定された既存の親プロジェクトの下に、指定された名前のサブプロジェクトを作成し `lpParentProjPath` ます。

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

からソース管理プラグインのコンテキストポインター。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力]ユーザー名 (NULL 終端文字を含む SCC_USER_SIZE まで)。

 lpParentProjPath

から親プロジェクトのパスを識別する文字列 (NULL ターミネータを含む SCC_PRJPATH_SIZE まで)。

 lpSubProjName

から推奨されるサブプロジェクト名 (NULL 終端文字を含む SCC_PRJPATH_SIZE まで)。

 lpAuxProjPath

[入力、出力]プロジェクトを識別する補助文字列 (NULL ターミネータを含む SCC_PRJPATH_SIZE まで)。

 lpSubProjPath

[入力、出力]サブプロジェクトのパスを識別する出力文字列 (NULL ターミネータを含む SCC_PRJPATH_SIZE まで)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|サブプロジェクトが正常に作成されました。|
|SCC_E_INITIALIZEFAILED|親プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーは、ソース管理システムにログインできませんでした。|
|SCC_E_COULDNOTCREATEPROJECT|サブプロジェクトを作成できません。|
|SCC_E_PROJSYNTAXERR|プロジェクトの構文が無効です。|
|SCC_E_UNKNOWNPROJECT|親プロジェクトは、ソース管理プラグインでは不明です。|
|SCC_E_INVALIDFILEPATH|ファイルパスが無効であるか、使用できません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_CONNECTIONFAILURE|ソース管理プラグイン接続の問題が発生しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>注釈
 同じ名前のサブプロジェクトが既に存在する場合、関数は、既定の名前を変更して一意の名前を作成できます。たとえば、"_ \<number> " を追加します。 、、およびへの変更を受け入れるには、呼び出し元が準備されている必要があり `lpUser` `lpSubProjPath` `lpAuxProjPath` ます。 次に、 `lpSubProjPath` `lpAuxProjPath` 引数と引数を [Sccopenproject](../extensibility/sccopenproject-function.md)の呼び出しで使用します。 返されるときに、呼び出し元によって変更されないようにする必要があります。 これらの文字列は、ソース管理プラグインがプロジェクトに関連付けるために必要な情報を追跡するための手段を提供します。 呼び出し元 IDE では、これらの2つのパラメーターは返されません。これは、プラグインが表示に適さない可能性のある書式設定された文字列を使用できるためです。 関数は成功または失敗のコードを返し、成功した場合は、 `lpSubProjPath` 新しいプロジェクトへの完全なプロジェクトパスを変数に入力します。

 この関数は [Sccgetprojpath](../extensibility/sccgetprojpath-function.md)に似ていますが、ユーザーに選択を求めるのではなく、プロジェクトが自動的に作成される点が異なります。 `SccCreateSubProject`関数が呼び出されると、 `lpParentProjName` と `lpAuxProjPath` は空にならず、有効なプロジェクトに対応します。 これらの文字列は、通常、以前の `SccGetProjPath` 関数または [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)の呼び出しから IDE によって受信されます。

 `lpUser`引数はユーザー名です。 IDE は、以前に受信したものと同じユーザー名を渡します `SccGetProjPath` 。ソース管理プラグインでは、その名前を既定値として使用する必要があります。 ユーザーが既にプラグインと開いている接続を持っている場合、プラグインは、関数がサイレントモードで動作するかどうかを確認するプロンプトを表示しないようにする必要があります。 ただし、ログインに失敗した場合は、プラグインによってユーザーにログインを求めるメッセージが表示され、有効なログインを受け取ったときに、その名前がに戻され `lpUser` ます。 この文字列はプラグインによって変更される可能性があるため、IDE は常にサイズのバッファー (SCC_USER_LEN + 1 または SCC_USER_SIZE (null 終端文字用の領域を含む) を割り当てます。 文字列が変更された場合、新しい文字列は有効なログイン名 (少なくとも古い文字列と同じ) である必要があります。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject と SccGetParentProjectPath のテクニカルノート
 Visual Studio では、ソース管理システムでの場所の選択を求めるメッセージが表示される回数を最小限に抑えるために、Visual Studio でソリューションとプロジェクトを簡単に追加できました。 ソース管理プラグインが新しい関数との両方をサポートしている場合、これらの変更は Visual Studio によってアクティブ化され `SccCreateSubProject` `SccGetParentProjectPath` ます。 ただし、次のレジストリエントリを使用すると、これらの変更を無効にして、以前の Visual Studio (ソース管理プラグイン API バージョン 1.1) の動作に戻すことができます。

 **[HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateSolutionRootFolderInSourceControl" = dword: 00000001**

 このレジストリエントリが存在しない場合、または dword: 00000000 に設定されている場合、Visual Studio は、新しい関数、およびを使用しようとし `SccCreateSubProject` `SccGetParentProjectPath` ます。

 レジストリエントリが dword: 00000001 に設定されている場合、Visual Studio はこれらの新しい関数を使用しません。また、ソース管理に追加する操作は、以前のバージョンの Visual Studio の場合と同様に動作します。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
