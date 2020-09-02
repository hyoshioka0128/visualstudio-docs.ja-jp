---
title: EditorConfig
description: EditorConfig ファイルを使用し、Visual Studio for Mac でプロジェクト コードを一貫性のあるスタイルで記述します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.technology: vs-ide-install
ms.assetid: 26A0DE31-2FBF-4E1B-99FB-083111AA1680
ms.openlocfilehash: be8f508a0055d4cd7cbacf1c728e6d73c8b281f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74984722"
---
# <a name="creating-and-editing-a-custom-editorconfig-file"></a>カスタム EditorConfig ファイルの作成と編集

Visual Studio for Mac では、[EditorConfig](https://editorconfig.org/) ファイルをプロジェクトまたはソリューションに追加して、そのコードベースを使用するすべてのユーザーに一貫したコーディング スタイルを使用させることができます。 EditorConfig ファイルで宣言された設定は、Visual Studio for Mac テキスト エディターのグローバルな設定より優先されます。 プロジェクトまたはコードベース内で EditorConfig ファイルを使用すると、プロジェクトのコード記述スタイル、優先設定、警告を設定できます。 このファイルはコードベースの一部であるため、すべてのユーザーが使用している IDE またはコード エディターに関わらず、より容易にプロジェクトのコーディング方法に従うことができます。

[EditorConfig](https://editorconfig.org/) ファイルは、Visual Studio 2017 など、さまざまな IDE やコード エディターでサポートされています。

## <a name="supported-settings"></a>サポートされる設定

Visual Studio for Mac のエディターは、[EditorConfig プロパティ](https://editorconfig.org/#supported-properties)の次のコア セットをサポートしています。

- `indent_style`
- `indent_size`
- `tab_width`
- `end_of_line`
- `charset`
- `trim_trailing_whitespace`
- `insert_final_newline`
- `root`

EditorConfig は、C# の[コーディング規則](/visualstudio/ide/editorconfig-code-style-settings-reference)もサポートしています。

## <a name="add-an-editorconfig-file-to-a-project"></a>EditorConfig ファイルをプロジェクトに追加する

### <a name="adding-a-new-editorconfig-file"></a>新しい EditorConfig ファイルを追加する

1. Visual Studio for Mac でプロジェクトを開きます。 EditorConfig ファイルを追加するソリューションまたはプロジェクト ノードのいずれかを選択します。 ソリューション ディレクトリにファイルを追加すると、ソリューション内のすべてのプロジェクトに .editorconfig の設定が適用されます。

2. ノードを右クリックして **[追加]、[新しいファイル]** の順に選択し、 **[新しいファイル]** ダイアログを開きます。

    ![コンテンツ メニュー項目](media/editorconfig-image0.png)

3. **[その他]、[空のテキスト ファイル]** の順に選択し、`.editorconfig` という **[名前]** を付けます。 **[新規作成]** を押してファイルを作成し、エディターで開きます。

    ![[新しいファイル] ダイアログ](media/editorconfig-image1.png)

    項目をソリューション レベルで追加すると、項目が **[ソリューション項目]** フォルダーに自動的に作成および追加されます。

    ![ソリューション パッドに表示されているソリューション項目](media/editorconfig-image1a.png)

4. ファイルを編集します。 次に例を示します。

    ```EditorConfig
    # This file is the top-most EditorConfig file
    root = true

    # All Files
    [*]
    indent_style = space
    indent_size = 8
    insert_final_newline = false
    trim_trailing_whitespace = false

    [*.cs]
    csharp_new_line_before_open_brace = none
    ```

4. `.editorconfig` ファイルの設定は、ユーザーが記述するすべての新しいコードに適用されますが、既存のコードを新しい設定にするには、それを再フォーマットする必要があります。 既存のソース ファイルに `.editorconfig` ファイルの設定を反映させるには、ファイルを開き、メニュー バーから **[編集]、[形式]、[ドキュメントのフォーマット]** の順に選択します。

    ![[ドキュメントのフォーマット] メニュー アイテム](media/editorconfig-image2.png)

### <a name="adding-an-existing-editorconfig-file"></a>既存の EditorConfig ファイルを追加する

`.editorconfig` ファイルが既に含まれているプロジェクトかソリューションを使用している場合、設定の適用に必要な作業はありません。 新しいコード行はすべて、EditorConfig の設定に従って書式設定されます。

プロジェクトの既存の `.editorconfig` ファイルを再利用すると便利な場合があります。 既存のファイルを追加するには、次を実行します。

1. それを追加するフォルダーを右クリックし、 **[追加]、[ファイルの追加]** の順に選択します。

2. 必要なファイルのディレクトリに移動します。

3. macOS では、(`.editorconfig` などの) `.` で始まるファイルは隠しファイルであるため、**Command + Shift + .** を押して `.editorconfig` ファイルを表示します。

4. `.editorconfig` ファイルを選択し、 **[開く]** をクリックします。

    ![新しいファイルを追加するウィンドウ](media/editorconfig-image3b.png)

5. 次のダイアログが表示されたら、 **[ファイルをディレクトリにコピーする]** オプションを選択し、 **[OK]** を選択します。

    ![[ファイルをフォルダーに追加する] ダイアログ オプション](media/editorconfig-image3.png)

### <a name="reflecting-editorconfig-settings"></a>.editorconfig の設定を反映する

コードベースに EditorConfig ファイルを追加したら、追加したすべてのコードは、指定した設定どおりに自動的にフォーマットされます。 コードベースをフォーマットしない限り、既存のコードには、設定は自動的には反映されません。

`.editorconfig` ファイルの設定を反映させるには、ソリューション ノードを選択し、メニュー バーから **[編集]、[形式]、[ドキュメントのフォーマット]** の順に選択します。

![メニュー バーからドキュメントをフォーマットする](media/editorconfig-image3a.png)

## <a name="editing-an-editorconfig-file"></a>EditorConfig ファイルを編集する

EditorConfig ファイルでは、単純なファイル レイアウトを利用し、設定を指定します。前の例を利用して説明すると下のようになります。

```EditorConfig
# This file is the top-most EditorConfig file
root = true

# All Files
[*]
indent_style = space
indent_size = 4
insert_final_newline = false
trim_trailing_whitespace = false

[*.cs]
csharp_new_line_before_open_brace = none
```

「[EditorConfig 設定のオーバーライド](#override-editorconfig-settings)」セクションに説明されているように、`root` を `true` に設定すると、このファイルがコードベースの一番上のファイルとしてフラグを設定され、プロジェクトでそれより上の `.editorconfig` ファイルは無視されます。

各セクションには角括弧 ( **[ ]** ) が付き、後続のプロパティが付属するファイルの型に関する情報が指定されます。

上の例では、一部の設定がプロジェクトのすべてのファイルに適用されます。その他の設定は C# ファイルにのみ追加されます。 下のスクリーンショットでは、`.editorconfig` 設定の適用前後を確認できます。

**適用前**:

![EditorConfig 設定の適用前](media/editorconfig-image4.png)

**適用後**:

![EditorConfig 設定の適用後](media/editorconfig-image5.png)

利用できる EditorConfig 設定に関する詳細については、「[EditorConfig の .NET コーディング規則の設定](/visualstudio/ide/editorconfig-code-style-settings-reference)」という記事と、公式ドキュメントの[サポート プロパティ](https://editorconfig.org/#supported-properties)に関するセクションを参照してください。

## <a name="override-editorconfig-settings"></a>EditorConfig 設定のオーバーライド

各ソリューションに複数の `.editorconfig` ファイルを与えることができます。 Visual Studio for Mac は、ソリューションで上から下へと `.editorconfig` ファイルを読み込みながら、設定を追加およびオーバーライドします。これは、編集しているファイルに_最も近い_ `.editorconfig` の設定が優先されることを意味します。 設定は、(存在する場合) 同じフォルダーの `.editorconfig` ファイルから、次いで (存在する場合) 親フォルダーなどの `.editorconfig` から取得されます。 これは、`root=true` が見つかるまで実行されます。

すべての上位レベルの `.editorconfig` ファイルからの設定がコードベースのこの部分に適用_されない_ようにするには、次のように `root=true` プロパティを下位レベルの `.editorconfig` ファイルに追加します。

```EditorConfig
# top-most EditorConfig file
root = true
```

## <a name="see-also"></a>関連項目

- [EditorConfig でカスタム エディター設定を作成する (Windows の Visual Studio)](/visualstudio/ide/create-portable-custom-editor-options)