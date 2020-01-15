---
title: EditorConfig 設定
ms.date: 08/01/2018
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: a3aee4945b4a3b41a7f6ec532268c2c19f549d0a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589787"
---
# <a name="create-portable-custom-editor-settings-with-editorconfig"></a>EditorConfig で移植可能なカスタム エディター設定を作成する

[EditorConfig](https://editorconfig.org/) ファイルをプロジェクトまたはコードベースに追加して、そのコードベースを使用するすべてのユーザーに一貫したコーディング スタイルを使用させることができます。 EditorConfig の設定は、Visual Studio テキスト エディターのグローバルな設定より優先されます。 つまり、そのプロジェクトに固有のテキスト エディター設定を使用するように各コードベースを調整できます。 その場合でも、ユーザーは Visual Studio の **[オプション]** ダイアログ ボックスで、エディターを個人用に設定することができます。 個人設定は、 *.editorconfig* ファイルのないコードベースで作業している場合、または *.editorconfig* ファイルが特定の設定をオーバーライドしない場合に、常に適用されます。 このような個人設定の一例が、インデント スタイル (タブまたはスペース) です。

EditorConfig の設定は、Visual Studio など、多くのコード エディターと IDE でサポートされています。 この設定は、コードと共に移動する移植可能なコンポーネントであり、Visual Studio の外部であってもコーディング スタイルを適用できます。

::: moniker range=">=vs-2019"

Visual Studio でプロジェクトに EditorConfig ファイルを追加すると、新しいコード行は EditorConfig 設定に従って書式設定されます。 次のコマンドのいずれかを実行しない限り、既存コードの書式設定は変更されません。

 - [[コードのクリーンアップ]](../ide/code-styles-and-code-cleanup.md) (**Ctrl**+**K**、**Ctrl**+**E**)。あらゆる空白設定 (インデント スタイルなど) と選択されているコード スタイル設定 (`using` ディレクティブの並べ替え方法など) が適用されます。
 - **[編集]** > **[詳細]** > **[ドキュメントのフォーマット]** (または **Ctrl**+**K**、既定のプロファイルの場合は **Ctrl**+**D**)。インデント スタイルなど、空白設定のみが適用されます。

 ::: moniker-end

::: moniker range="=vs-2017"

Visual Studio でプロジェクトに EditorConfig ファイルを追加すると、新しいコード行は EditorConfig 設定に従って書式設定されます。 ドキュメントの書式を設定しない限り、既存のコードの書式設定は変更されません (既定のプロファイルの場合は **[編集]**  >  **[詳細設定]**  >  **[ドキュメントのフォーマット]** 、または **Ctrl**+**K**、**Ctrl**+**D**)。 [追加のコード クリーンアップを実行する](../ide/code-styles-and-code-cleanup.md#apply-code-styles)ように [ドキュメントのフォーマット] を構成していない限り、ドキュメントをフォーマットしても影響を受けるのはインデント スタイルなどの空白設定だけです。

 ::: moniker-end

::: moniker range="vs-2017"

[ **[書式設定]** オプション ページ](reference/options-text-editor-csharp-formatting.md#format-document-settings)で、**ドキュメントのフォーマット**で適用する EditorConfig 設定を定義することができます。

::: moniker-end

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac の EditorConfig](/visualstudio/mac/editorconfig) に関するページを参照してください。

## <a name="code-consistency"></a>コードの整合性

EditorConfig ファイルの設定を利用すれば、使用するエディターや IDE に関係なく、コードベースでコーディングのスタイルと設定の一貫性を維持できます。たとえば、インデントのスタイル、タブの幅、行末文字、エンコードなどです。 たとえば、C# でコーディングするとき、インデントを常に 5 つ分の空白文字で構成し、文書で UTF-8 エンコードを使用し、各行が常に CR/LF で終わるというという慣習をコードベースに与えるのであれば、そのように *.editorconfig* ファイルを構成できます。

個人的なプロジェクトで使用するコーディング規則は、チームのプロジェクトで使用するそれとは変えることができます。 たとえば、コーディングの際に、自分はインデントでタブ文字を追加したくても、 チームはインデントでタブ文字ではなく 4 つの空白文字を追加したいかもしれません。 EditorConfig ファイルがこの問題を解決します。シナリオごとに構成を与えることができるからです。

設定はコードベースのファイルに含まれているため、そのコードベースと共に移動します。 EditorConfig 対応のエディターでコード ファイルを開く限り、テキスト エディター設定が実装されます。 EditorConfig ファイルの詳細については、[EditorConfig.org](https://editorconfig.org/) Web サイトをご覧ください。

> [!NOTE]
> EditorConfig ファイルで設定されている規則は、現時点ではビルド エラーまたは警告として CI/CD パイプラインに適用できません。 すべてのスタイルの逸脱は、Visual Studio エディターと**エラー一覧**でのみ表示されます。

## <a name="supported-settings"></a>サポートされる設定

Visual Studio のエディターは、[EditorConfig プロパティ](https://editorconfig.org/#supported-properties)の次のコア セットをサポートします。

- indent_style
- indent_size
- tab_width
- end\_of_line
- charset
- trim\_trailing_whitespace
- insert\_final_newline
- root

EditorConfig エディター設定は、XML を除き、Visual Studio 対応のすべての言語でサポートされています。 また、EditorConfig では、C# および Visual Basic に対する[言語](../ide/editorconfig-language-conventions.md)、[書式](../ide/editorconfig-formatting-conventions.md)、[名前付け](../ide/editorconfig-naming-conventions.md)の規則など、[コード スタイル](../ide/editorconfig-code-style-settings-reference.md)の規則がサポートされています。

## <a name="add-and-remove-editorconfig-files"></a>EditorConfig ファイルの追加と削除

プロジェクトまたはコードベースに EditorConfig ファイルを追加すると、記述した新しいコード行は、EditorConfig ファイルに従って書式設定されます。 ただし、EditorConfig ファイルを追加しても、ドキュメントを書式設定するか、[[コードのクリーンアップ]](../ide/code-styles-and-code-cleanup.md) を実行するまでは、既存のスタイルが新しいスタイルに変換されることはありません。 たとえば、タブで書式設定されているインデントがファイル内にあり、スペースでインデントする EditorConfig ファイルを追加する場合、インデント文字は自動的にスペースに変換されません。 ドキュメントの書式を設定すると ( **[編集]**  >  **[詳細設定]**  >  **[ドキュメントのフォーマット]** 、または **Ctrl**+**K**、**Ctrl**+**D**)、EditorConfig ファイルの空白設定が既存のコード行に適用されます。

EditorConfig ファイルをプロジェクトまたはコードベースから削除し、新しいコード行がグローバル エディターの設定に従って書式設定されるようにする場合は、開いているコード ファイルをすべて閉じてから再度開く必要があります。

### <a name="add-an-editorconfig-file-to-a-project"></a>EditorConfig ファイルをプロジェクトに追加する

1. Visual Studio でプロジェクトまたはソリューションを開きます。 *.editorconfig* 設定をソリューションのすべてのプロジェクトに適用するか、1 つのプロジェクトだけに適用するかに応じて、プロジェクト ノードまたはソリューション ノードのいずれかを選択します。 また、 *.editorconfig* ファイルを追加するプロジェクトまたはソリューションで、フォルダーを選択できます。

1. メニュー バーから **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択するか、**Ctrl**+**Shift**+**A** キーを押します。

   **[新しい項目の追加]** ダイアログ ボックスが開きます。

1. 検索ボックスで、**editorconfig** を検索します。

   2 つの **editorconfig ファイル**項目テンプレートが、検索結果に表示されます。

   ![Visual Studio の EditorConfig ファイル項目テンプレート](media/editorconfig-item-templates.png)

1. **editorconfig ファイル (既定)** テンプレートを選択し、インデント スタイルとサイズに対する 2 つのコア EditorConfig オプションが設定されている EditorConfig ファイルを追加します。 または、**editorconfig ファイル (.NET)** テンプレートを選択し、既定の [.NET コード スタイル、書式、および名前付けの規則](../ide/editorconfig-code-style-settings-reference.md)が設定されている EditorConfig ファイルを追加します。

   ソリューション エクスプローラーに *.editorconfig* ファイルが表示されたら、エディターで開きます。

   ![ソリューション エクスプローラーとエディターの .editorconfig ファイル](media/editorconfig-dotnet.png)

1. 必要に応じてファイルを編集します。

### <a name="other-ways-to-add-an-editorconfig-file"></a>EditorConfig ファイルを追加するその他の方法

EditorConfig ファイルをプロジェクトに追加する方法は、他にもいくつかあります。

- Visual Studio 用 IntelliCode の[コード推論機能](/visualstudio/intellicode/code-style-inference)では、既存のコードからコードのスタイルが推論されます。 その後、既に定義されているコード スタイルの設定で、空ではない EditorConfig ファイルが作成されます。

- Visual Studio 2019 以降では、 **[ツール]**  >  **[オプション]** の[コード スタイルの設定に基づいて EditorConfig ファイルを生成する](/visualstudio/ide/code-styles-and-code-cleanup#code-styles-in-editorconfig-files)ことができます。

## <a name="file-hierarchy-and-precedence"></a>ファイルの階層と優先順位

ファイル階層のフォルダーに *.editorconfig* ファイルを追加すると、その設定がその階層レベルとその下のレベルのあらゆる該当ファイルに適用されます。 また、特定のプロジェクトやコードベースの EditorConfig 設定をオーバーライドしたり、コードベースの一部の EditorConfig 設定をオーバーライドして、コードベースの他の部分とは異なる規則を使用するようにしたりできます。 これは、別の場所からコードを組み込んで、その規則を変更したくない場合に役立ちます。

一部またはすべての EditorConfig 設定をオーバーライドするには、オーバーライドされた設定を適用するファイルの階層レベルに *.editorconfig* ファイルを追加します。 新しい EditorConfig ファイルの設定は、同じレベルと任意のサブディレクトリ内のファイルに適用されます。

![EditorConfig 階層](../ide/media/vside_editorconfig_hierarchy.png)

すべての設定ではなく一部をオーバーライドする場合には、 *.editorconfig* ファイルで該当する設定だけを指定します。 下位レベルのファイルで明示的に一覧表示したプロパティのみがオーバーライドされます。 上位レベルの *.editorconfig* ファイルからのその他の設定は、引き続き適用されます。 _すべての_上位レベルの *.editorconfig* ファイルからの設定がコードベースのこの部分に適用_されない_ようにするには、次のように ```root=true``` プロパティを下位レベルの *.editorconfig* ファイルに追加します。

```ini
# top-most EditorConfig file
root = true
```

EditorConfig ファイルは上から下に読み取られます。 同じ名前のプロパティが複数ある場合は、その名前の最も最近見つかったプロパティが優先されます。

## <a name="edit-editorconfig-files"></a>EditorConfig ファイルの編集

Visual Studio では、 *.editorconfig* ファイルを編集しやすいように、IntelliSense の入力候補一覧が提供されます。

![.editorconfig ファイルの IntelliSense](media/editorconfig-intellisense-no-extension.png)

EditorConfig ファイルを編集したら、コード ファイルを再度読み込んで新しい設定を有効にする必要があります。

多数の *.editorconfig* ファイルを編集する場合は、[EditorConfig 言語サービス拡張機能](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig)が便利です。 この拡張機能には、構文の強調表示、強化された IntelliSense、検証、およびコードの書式設定などの機能が含まれます。

![EditorConfig 言語サービス拡張機能の IntelliSense](media/editorconfig-intellisense.png)

## <a name="example"></a>例

次の例では、 *.editorconfig* ファイルをプロジェクトに追加する前と追加した後の C# コード スニペットのインデント状態を示します。 Visual Studio テキスト エディターの **[オプション]** ダイアログ ボックスにある **[タブ]** 設定は、**Tab** キーを押したときに空白文字を入力するように設定されています。

![テキスト エディター タブの設定](../ide/media/vside_editorconfig_tabsetting.png)

設定どおり、次の行で **Tab** キーを押すと、4 つ分の空白文字が追加されてインデントが行われます。

![EditorConfig を使用する前のコード](../ide/media/vside_editorconfig_before.png)

*.editorconfig* という名前の新しいファイルを、次のコンテンツと共にプロジェクトに追加します。 `[*.cs]` の設定は、この変更がこのプロジェクトの C# コード ファイルにのみ適用されることを意味します。

```ini
# Top-most EditorConfig file
root = true

# Tab indentation
[*.cs]
indent_style = tab
```

これで、**Tab** キーを押すと、スペースの代わりにタブ文字が入力されます。

![Tab キーでタブ文字が追加されます](../ide/media/vside_editorconfig_tab.png)

## <a name="troubleshoot-editorconfig-settings"></a>EditorConfig 設定のトラブルシューティング

EditorConfig ファイルがディレクトリ構造内でプロジェクトの場所と同じか上位にある場合、Visual Studio はそのファイル内のエディター設定をエディターに適用します。 この場合、ステータス バーに次のメッセージが表示される場合があります。

   "**このファイルの種類のユーザー設定は、このプロジェクトのコーディング規則によりオーバーライドされます。** "

つまり、 **[ツール]** 、 >  **[オプション]** 、 >  **[テキスト エディター]** の任意のエディター設定 (インデントのサイズとスタイル、タブ サイズ、コーディング規則など) が、ディレクトリ構造内でプロジェクトと同じか上位にある EditorConfig ファイルで指定されると、EditorConfig ファイル内の規則が**オプション**の設定をオーバーライドします。 この動作は、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]** の **[プロジェクトのコーディング規則に従います]** オプションを切り替えることで制御できます。 このオプションをオフにすると、Visual Studio の EditorConfig に対するサポートが無効になります。

![[ツール] メニューの [オプション] - [プロジェクトのコーディング規則に従います]](media/coding_conventions_option.png)

親ディレクトリで任意の *.editorconfig* ファイルを見つけるには、コマンド プロンプトを開き、プロジェクトが格納されているディスクのルートから次のコマンドを実行します。

```Shell
dir .editorconfig /s
```

EditorConfig 規則の範囲を制御するには、リポジトリのルートにある、またはプロジェクトが格納されているディレクトリ内の *.editorconfig* ファイルで ```root=true``` プロパティを設定します。 Visual Studio は、開かれたファイルのディレクトリ内とすべての親ディレクトリで *.editorconfig* という名前のファイルを探します。 検索は、ルート ファイル パスに到達するか、または ```root=true``` を含む *.editorconfig* ファイルが見つかると、終了します。

## <a name="see-also"></a>関連項目

- [.NET コード表記規則](../ide/editorconfig-code-style-settings-reference.md)
- [言語サービスの EditorConfig のサポート](../extensibility/supporting-editorconfig.md)
- [EditorConfig.org](https://editorconfig.org/)
- [コード エディターの機能](writing-code-in-the-code-and-text-editor.md)
- [EditorConfig (Visual Studio for Mac)](/visualstudio/mac/editorconfig)
