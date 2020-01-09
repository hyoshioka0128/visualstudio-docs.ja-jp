---
title: 外部ツールの管理
ms.date: 11/20/2017
ms.topic: conceptual
f1_keywords:
- vs.externaltools
helpviewer_keywords:
- external tools [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0f22c687f88c7736d5c088ebc28ff490c4c16b8f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591295"
---
# <a name="manage-external-tools"></a>外部ツールの管理

Visual Studio から **[ツール]** メニューを使用して外部ツールを呼び出すことができます。 **[ツール]** メニューではいくつかのツールを既定で使用できますが、このメニューは他の独自の実行可能ファイルを追加してカスタマイズできます。

## <a name="tools-available-on-the-tools-menu"></a>[ツール] メニューで使用できるツール

**[ツール]** メニューには、次のような複数の組み込みコマンドが含まれます。

::: moniker range="vs-2017"

* **[拡張機能と更新プログラム]** [Visual Studio 拡張機能を管理する](finding-and-using-visual-studio-extensions.md)
* **[コード スニペット マネージャー]** [コード スニペットを整理する](code-snippets.md)
* **[カスタマイズ]** [メニューおよびツール バーをカスタマイズする](how-to-customize-menus-and-toolbars-in-visual-studio.md)
* **[オプション]** [Visual Studio IDE と他のツールの多様なオプションを設定する](reference/options-dialog-box-visual-studio.md)

::: moniker-end

::: moniker range=">=vs-2019"

* **[コード スニペット マネージャー]** [コード スニペットを整理する](code-snippets.md)
* **[カスタマイズ]** [メニューおよびツール バーをカスタマイズする](how-to-customize-menus-and-toolbars-in-visual-studio.md)
* **[オプション]** [Visual Studio IDE と他のツールの多様なオプションを設定する](reference/options-dialog-box-visual-studio.md)

::: moniker-end

## <a name="add-new-tools-to-the-tools-menu"></a>[ツール] メニューに新しいツールを追加する

**[ツール]** メニューに表示する外部ツールを追加できます。

1. **[ツール]** 、 **[外部ツール]** の順に選択し、 **[外部ツール]** ダイアログ ボックスを開きます。

1. **[追加]** をクリックして情報を入力します。 たとえば、次のエントリを指定すると、Visual Studio で現在開いているファイルのディレクトリで**エクスプローラー**が開きます。

   * タイトル: `Open File Location`

   * コマンド: `explorer.exe`

   * 引数: `/root, "$(ItemDir)"`

   ![[外部ツール] ダイアログ ボックス](media/external-tools-dialog.png)

外部ツールの定義時に使用できる引数の一覧を次に示します。

|名前|引数|説明|
|----------|--------------|-----------------|
|項目のパス|$(ItemPath)|現在のファイルの完全なファイル名 (ドライブ + パス + ファイル名)。|
|項目のディレクトリ|$(ItemDir)|現在のファイルのディレクトリ (ドライブ + パス)。|
|項目のファイル名|$(ItemFilename)|現在のファイルのファイル名 (ファイル名)。|
|項目の拡張子|$(ItemExt)|現在のファイルのファイル名拡張子。|
|カレント行|$(CurLine)|コード ウィンドウ内のカーソルの現在の行位置。|
|カレント列|$(CurCol)|コード ウィンドウ内のカーソルの現在の列位置。|
|カレント テキスト|$(CurText)|選択されているテキスト。|
|ターゲット パス|$(TargetPath)|作成するアイテムの完全なファイル名 (ドライブ + パス + ファイル名)。|
|ターゲット ディレクトリ|$(TargetDir)|作成するアイテムのディレクトリ。|
|ターゲット名|$(TargetName)|作成するアイテムのファイル名。|
|ターゲットの拡張子|$(TargetExt)|作成するアイテムのファイル名拡張子。|
|バイナリ ディレクトリ|$(BinDir)|作成中のバイナリの最終的な場所 (ドライブ + パスとして定義されます)。|
|プロジェクト ディレクトリ|$(ProjectDir)|現在のプロジェクトのディレクトリ (ドライブ + パス)。|
|プロジェクト ファイル名|$(ProjectFileName)|現在のプロジェクトのファイル名 (ドライブ + パス + ファイル名)。|
|ソリューション ディレクトリ|$(SolutionDir)|現在のソリューションのディレクトリ (ドライブ + パス)。|
|ソリューション ファイル名|$(SolutionFileName)|現在のソリューションのファイル名 (ドライブ + パス + ファイル名)。|

> [!NOTE]
> IDE のステータス バーに、アクティブな**コード エディター**の挿入位置を示す、**Current Line** 変数と **Current Column** 変数が表示されます。 **Current Text** 変数は、その場所で選択されているテキストまたはコードを返します。

## <a name="see-also"></a>関連項目

- [C/C++ のビルド ツール](/cpp/build/reference/c-cpp-build-tools)
