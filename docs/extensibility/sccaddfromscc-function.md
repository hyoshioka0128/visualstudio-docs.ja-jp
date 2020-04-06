---
title: 関数の追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1dd32e31330cdce958e463a40a4d92f88b09afb2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701246"
---
# <a name="sccaddfromscc-function"></a>関数の追加
この関数を使用すると、ユーザーはソース管理システムに既に存在するファイルを参照し、その後、それらのファイルを現在のプロジェクトの一部にすることができます。 たとえば、この関数は、ファイルをコピーせずに、現在のプロジェクトに共通のヘッダー ファイルを取得できます。 ファイルの戻り値の`lplpFileNames`配列には、ユーザーが IDE プロジェクトに追加するファイルのリストが含まれます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAddFromScc (
   LPVOID   pvContext,
   HWND     hWnd,
   LPLONG   lpnFiles,
   LPCSTR** lplpFileNames
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ファイル

[イン、アウト]追加されるファイルの数のバッファー。 (これは、`NULL`指すメモリ`lplpFileNames`が解放される場合です。 詳細については、「解説」を参照してください。

 ファイル名

[イン、アウト]ディレクトリ パスを持たないすべてのファイル名へのポインタの配列。 この配列は、ソース管理プラグインによって割り当てられ、解放されます。 = `lpnFiles` 1`lplpFileNames`で、`NULL`でない場合、指す配列の最初の名前`lplpFileNames`には、コピー先のフォルダーが含まれます。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|ファイルが正常に見つかり、プロジェクトに追加されました。|
|SCC_I_OPERATIONCANCELED|操作は無効にしてキャンセルされました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再ロードする必要があります。|

## <a name="remarks"></a>Remarks
 IDE はこの関数を呼び出します。 ソース管理プラグインがローカルの保存先フォルダの指定をサポートしている場合、IDE は`lpnFiles`= 1 を渡し、ローカル`lplpFileNames`フォルダ名を に渡します。

 関数の呼び出しが戻ると、プラグインは、`lpnFiles`に値を`lplpFileNames`割り当て、必要に応じてファイル名配列のメモリを割り当てられています (`lplpFileNames`この割り当ては 、 のポインタに置き換わります )。 `SccAddFromScc` ソース管理プラグインは、すべてのファイルをユーザーのディレクトリまたは指定フォルダに配置します。 その後、IDE によってファイルが IDE プロジェクトに追加されます。

 最後に、IDE はこの関数をもう一度呼び`NULL`出`lpnFiles`し、 に渡します。 これは、ファイル名配列に割り当てられたメモリを解放するために、ソース管理プラグインによって特別な信号として解釈されます。`lplpFileNames``.`

 `lplpFileNames`はポインタ`char ***`です。 ソース管理プラグインは、ファイル名へのポインターの配列へのポインターを配置するため、この API の標準的な方法でリストを渡します。

> [!NOTE]
> VSSCI API の初期バージョンでは、追加されたファイルのターゲット プロジェクトを示す方法が提供されませんでした。 これに対応するために、`lplpFIleNames`パラメータのセマンティクスが拡張され、出力パラメータではなく in/out パラメータにしました。 1 つのファイルだけを指定した場合、つまり= 1 が`lpnFiles`指す値は、 の最初の`lplpFileNames`要素にターゲット フォルダーが含まれます。 これらの新しいセマンティクスを使用するために、IDE`SccSetOption`はパラメーターを`nOption`に設定`SCC_OPT_SHARESUBPROJ`して関数を呼び出します。 ソース管理プラグインがセマンティクスをサポートしていない場合は、 を返します`SCC_E_OPTNOTSUPPORTED`。 これにより、**ソース管理から追加**機能の使用が無効になります。 プラグインが**ソース管理からの追加**機能 (`SCC_CAP_ADDFROMSCC`) をサポートしている場合は、新しいセマンティクスを`SCC_I_SHARESUBPROJOK`サポートし、 を返す必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
