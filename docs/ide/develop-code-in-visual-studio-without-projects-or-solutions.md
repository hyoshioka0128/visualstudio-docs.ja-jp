---
title: プロジェクトまたはソリューションを使用せずにコードを開発する
description: プロジェクトやソリューションを必要とせずに、Visual Studio で直接コードを開発する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/22/2020
ms.topic: how-to
helpviewer_keywords:
- open folder [Visual Studio]
- anycode [Visual Studio]
- projects and solutions, develop code without
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d706ccdc07abcc91e956878e1bc180be9c542223
ms.sourcegitcommit: 66cda27b63c9b55782b1db223a6dbda9f8cabe13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "95006004"
---
# <a name="develop-code-in-visual-studio-without-projects-or-solutions"></a>プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する

ほぼすべての種類のディレクトリ ベースのプロジェクトから、ソリューションまたはプロジェクト ファイルを使用せずに Visual Studio にコードを開くことができます。これは、たとえば、GitHub でリポジトリをクローンして、直接 Visual Studio に開き、ソリューションまたはプロジェクトを作成することなく開発を開始できることを意味します。必要な場合は、カスタム ビルド タスクを指定し、単純な JSON ファイルからパラメーターを起動できます。

Visual Studio でコード ファイルを開いた後、**ソリューション エクスプローラー** によって、フォルダー内のすべてのファイルが表示されます。 任意のファイルをクリックして、編集を開始できます。 バックグラウンドでは、Visual Studio は、ファイルのインデックス作成を開始して、IntelliSense、ナビゲーション、およびリファクタリング機能を有効にします。 ファイルを編集、作成、移動、または削除すると、Visual Studio は自動的に変更を追跡し、IntelliSense インデックスを継続的に更新します。 コードは、構文が色付けされて表示され、多くの場合、基本的な IntelliSense ステートメント入力候補を含みます。

## <a name="open-any-code"></a>コードを開く

Visual Studio でコードを開く方法は、次のとおりです。

- Visual Studio メニュー バーで、 **[ファイル]**  >  **[開く]**  >  **[フォルダー]** を選択して、コードの場所を参照します。

- コードを含むフォルダーのコンテキスト (右クリック) メニューで、 **[Visual Studio で開く]** コマンドを選択します。

::: moniker range="vs-2017"
- Visual Studio **スタート ページ** で **[フォルダーを開く]** を選択します。

    > [!IMPORTANT]
    > Visual Studio の **[スタート ページ]** から **[フォルダーを開く]** リンクを使用してすべてのコードを開くことはできません。 たとえば、コード ファイルがソリューションの一部として (つまり、.sln ファイルに) 保存されている場合、ここに記載されている他のオプションのいずれかを使用してコードを開く必要があります。

::: moniker-end

::: moniker range=">=vs-2019"
- スタート ウィンドウで **[フォルダーを開く]** リンクを選択します。

    > [!IMPORTANT]
    > Visual Studio のスタート ウィンドウから **[フォルダーを開く]** リンクを使用してすべてのコードを開くことはできません。 たとえば、コード ファイルがソリューションの一部として (つまり、.sln ファイルに) 保存されている場合、ここに記載されている他のオプションのいずれかを使用してコードを開く必要があります。

::: moniker-end

- キーボードのユーザーの場合は、Visual Studio で **Ctrl**+**shift** +**Alt**+**O** キーを押します。

- クローンされた GitHub リポジトリからコードを開きます。

### <a name="to-open-code-from-a-cloned-github-repo"></a>クローンされた GitHub リポジトリからコードを開くには

次の例は、GitHub リポジトリをクローンし、Visual Studio でそのコードを開く方法を示しています。 この手順を実行するには、GitHub アカウントがあり、システム上に Git for Windows がインストールされている必要があります。 詳しくは、「[Signing up for a new GitHub account (GitHub アカウントに登録する)](https://help.github.com/articles/signing-up-for-a-new-github-account/)」および「[Git for Windows](https://git-for-windows.github.io/)」をご覧ください。

1. GitHub のクローンするリポジトリに移動します。

2. **[Clone or Download]\(クローンまたはダウンロード\)** ボタンをクリックし、ドロップダウン メニューで **[クリップボードにコピー]** ボタンを選択して、GitHub リポジトリのセキュリティ保護された URL をコピーします。

   ![GitHub の複製ボタン](./media/VSIDE_Code_Clone.png)

1. Visual Studio で、 **[チーム エクスプローラー]** タブを選択し、**チーム エクスプローラー** を開きます。 タブが表示されない場合は、 **[ビュー]**  >  **[チーム エクスプローラー]** からタブを開きます。

1. チーム エクスプローラーの **[ローカル Git リポジトリ]** セクションで **[クローン]** コマンドを選択し、GitHub ページの URL をテキスト ボックスに貼り付けます。

   ![プロジェクトの複製](./media/VSIDE_Code_Clone2.png)

5. **[クローン]** ボタンを選択して、プロジェクトのファイルをローカル Git リポジトリにクローンします。リポジトリのサイズによっては、この処理に数分かかることがあります。

1. リポジトリがシステムに複製されたら、**チーム エクスプローラー** で、新しく複製されたリポジトリのコンテキスト (右クリック) メニューで **[開く]** コマンドを選択します。

   ![複製されたリポジトリ](./media/VSIDE_Code_Clone3.png)

1. **[フォルダー ビューの表示]** コマンドを選択して、**ソリューション エクスプローラー** でファイルを表示します。

   ![フォルダー ビューの表示](./media/VSIDE_Code_Clone3_show.png)

   クローンされたリポジトリでフォルダーとファイルを参照したり、Visual Studio コード エディターでコードを表示/検索したり、構文の色付けなどの機能でコードを補完したりできるようになりました。

## <a name="run-and-debug-your-code"></a>コードを実行してデバッグする

Visual Studio でプロジェクトまたはソリューションを使用せずにコードをデバッグすることができます。 一部の言語では、コード ベースで有効な "*スタートアップ ファイル*" (スクリプト、実行可能ファイル、プロジェクトなど) の指定が必要になる場合があります。 ツールバーの **[開始]** ボタンの横にあるドロップダウン リスト ボックスに、Visual Studio によって検出されたすべてのスタートアップ アイテムと、明示的に指定した項目が一覧表示されます。 コードのデバッグ時に、このコードが Visual Studio によって最初に実行されます。

Visual Studio で実行するコードの構成は、そのコードの種類やビルド ツールに応じて異なります。

### <a name="codebases-that-use-msbuild"></a>MSBuild を使用するコードベース

MSBuild ベース コードベースでは、 **[開始]** ボタンのドロップダウン リストに表示される複数のビルド構成を保持できます。 スタートップ アイテムとして使用したいファイルを選び、 **[開始]** ボタンを選択してデバッグを開始します。

> [!NOTE]
> C# および Visual Basic コードベースの場合、 **.NET デスクトップ開発** のワークロードがインストールされている必要があります。 C++ コードベースの場合、**C++ によるデスクトップ開発** のワークロードがインストールされている必要があります。

### <a name="codebases-that-use-custom-build-tools"></a>カスタム ビルド ツールを使用するコードベース

お使いのコードベースでカスタム ビルド ツールを使用している場合、 *.json* ファイルに定義されている *ビルド タスク* を使用したコードの作成方法を Visual Studio に指示する必要があります。 詳細については、[ビルドのカスタマイズとタスクのデバッグ](../ide/customize-build-and-debug-tasks-in-visual-studio.md)に関するページをご覧ください。

### <a name="codebases-that-contain-python-or-javascript-code"></a>Python または JavaScript コードを含むコードベース

コードベースに Python または JavaScript コードが含まれている場合、 *.json* ファイルを構成する必要はありませんが、対応するワークロードをインストールする必要が生じます。 また、次のようにスタートアップ スクリプトを構成する必要があります。

1. **[ツール]**  >  **[ツールと機能を取得]** を選択するか、または Visual Studio を複製して Visual Studio インストーラーを実行して、[Node.js 開発](https://visualstudio.microsoft.com/vs/node-js/)または [Python 開発](https://visualstudio.microsoft.com/vs/python/)のワークロードをインストールします。

   ![Node.js および Python 開発のワークロード](media/python_nodejs_workloads.png)

1. **ソリューション エクスプローラー** で、JavaScript または Python ファイルを右クリックしたコンテキスト メニューで、 **[スタートアップ アイテムとして設定]** コマンドを選択します。

1. **[開始]** ボタンを選択して、デバッグを開始します。

### <a name="codebases-that-contain-c-code"></a>C++ コードを含むコードベース

Visual Studio のソリューションやプロジェクトを使用せずに C++ コードを開く場合の手順については、[C++ でフォルダーのプロジェクトを開く](/cpp/build/open-folder-projects-cpp)方法に関するページをご覧ください。

### <a name="codebases-that-contain-a-visual-studio-project"></a>Visual Studio プロジェクトを含むコードベース

コードのフォルダーに Visual Studio プロジェクトが含まれている場合、スタートアップ アイテムとしてプロジェクトを指定できます。

![スタートアップ アイテムとしてプロジェクトを設定する](media/customize-set-project-as-startup-item.png)

プロジェクトがスターアップ アイテムであることを反映して、 **[開始]** ボタンのテキストが変更されます。

![[開始] ボタンにあるプロジェクト](media/customize-start-button-project.png)

## <a name="see-also"></a>関連項目

- [ビルドのカスタマイズとタスクのデバッグ](../ide/customize-build-and-debug-tasks-in-visual-studio.md)
- [C++ でフォルダーのプロジェクトを開く](/cpp/build/open-folder-projects-cpp)
- [C++ での CMake プロジェクト](/cpp/build/cmake-projects-in-visual-studio)
- [コード エディターとテキスト エディターでのコードの作成](../ide/writing-code-in-the-code-and-text-editor.md)
