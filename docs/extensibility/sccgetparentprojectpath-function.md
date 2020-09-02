---
title: SccGetParentProjectPath 関数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700710"
---
# <a name="sccgetparentprojectpath-function"></a>SccGetParentProjectPath 関数
この関数は、指定されたプロジェクトの親プロジェクトパスを決定します。 この関数は、ユーザーが Visual Studio プロジェクトをソース管理に追加しているときに呼び出されます。

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

からソース管理プラグインのコンテキストポインター。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力]ユーザー名 (NULL ターミネータを含む SCC_USER_SIZE まで)。

 lpProjPath

からプロジェクトパスを識別する文字列 (NULL ターミネータを含む SCC_PRJPATH_SIZE まで)。

 lpAuxProjPath

[入力、出力]プロジェクトを識別する補助文字列 (NULL ターミネータを含む SCC_PRJPATH_SIZE まで)。

 lpParentProjPath

[入力、出力]親プロジェクトパス (NULL 終端文字を含む SCC_PRJPATH_SIZE まで) を識別する出力文字列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|親プロジェクトのパスが正常に取得されました。|
|SCC_E_INITIALIZEFAILED|プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーは、ソース管理プラグインにログインできませんでした。|
|SCC_E_UNKNOWNPROJECT|プロジェクトがソース管理プラグインに対して不明です。|
|SCC_E_INVALIDFILEPATH|ファイルパスが無効であるか、使用できません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_PROJSYNTAXERR|プロジェクトの構文が無効です。|
|SCC_E_CONNECTIONFAILURE|ストア接続の問題です。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>注釈
 この関数は成功または失敗のコードを返し、成功した場合は、 `lpParentProjPath` 指定されたプロジェクトの完全なプロジェクトパスを変数に入力します。

 この関数は、既存のプロジェクトの親プロジェクトパスを返します。 ルートプロジェクトの場合、関数は、渡されたプロジェクトパス (つまり、同じルートプロジェクトパス) を返します。 プロジェクトパスは、ソース管理プラグインに対してのみ意味のある文字列であることに注意してください。

 IDE では、パラメーターとパラメーターに対する変更も受け入れるように準備され `lpUser` `lpAuxProjPath` ています。 IDE はこれらの文字列を永続化し、ユーザーが後でこのプロジェクトを開いたときに [Sccopenproject](../extensibility/sccopenproject-function.md) に渡します。 したがって、これらの文字列は、ソース管理プラグインがプロジェクトに関連付けるために必要な情報を追跡するための手段を提供します。

 この関数は [Sccgetprojpath](../extensibility/sccgetprojpath-function.md)に似ていますが、プロジェクトを選択するようユーザーに求めるメッセージが表示される点が異なります。 また、新しいプロジェクトは作成されませんが、既存のプロジェクトでのみ動作します。

 `SccGetParentProjectPath`が呼び出されると、 `lpProjPath` とは空にならず、 `lpAuxProjPath` 有効なプロジェクトに対応します。 これらの文字列は、通常、以前の関数の呼び出しから IDE によって受信され `SccGetProjPath` ます。

 `lpUser`引数はユーザー名です。 IDE は、関数から以前に受信したものと同じユーザー名を渡し `SccGetProjPath` 、ソース管理プラグインはその名前を既定値として使用する必要があります。 ユーザーが既にプラグインと開いている接続を持っている場合、プラグインは、関数がサイレントモードで動作するかどうかを確認するプロンプトを表示しないようにする必要があります。 ただし、ログインに失敗した場合は、プラグインによってユーザーにログインを求めるメッセージが表示され、有効なログインを受け取ったときに、その名前がに戻され `lpUser` ます。 この文字列はプラグインによって変更される可能性があるため、IDE では常にサイズ (+ 1) のバッファーが割り当てられ `SCC_USER_LEN` ます。 文字列が変更された場合、新しい文字列は有効なログイン名 (少なくとも古い文字列と同じ) である必要があります。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject と SccGetParentProjectPath のテクニカルノート
 Visual Studio では、ソース管理システムでの場所の選択を求めるメッセージが表示される回数を最小限に抑えるために、Visual Studio でソリューションとプロジェクトを簡単に追加できました。 これらの変更は、ソース管理プラグインが新しい関数 [SccCreateSubProject](../extensibility/scccreatesubproject-function.md) と関数の両方をサポートしている場合、Visual Studio によってアクティブ化され `SccGetParentProjectPath` ます。 ただし、次のレジストリエントリを使用すると、これらの変更を無効にして、以前の Visual Studio (ソース管理プラグイン API バージョン 1.1) の動作に戻すことができます。

 **[HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateSolutionRootFolderInSourceControl" = dword: 00000001**

 このレジストリエントリが存在しない場合、または dword: 00000000 に設定されている場合、Visual Studio は、新しい関数、およびを使用しようとし `SccCreateSubProject` `SccGetParentProjectPath` ます。

 レジストリエントリが dword: 00000001 に設定されている場合、Visual Studio はこれらの新しい関数を使用しません。また、ソース管理に追加する操作は、以前のバージョンの Visual Studio の場合と同様に動作します。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
