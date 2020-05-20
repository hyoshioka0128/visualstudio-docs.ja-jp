---
title: Python コードの編集
description: Python の場合、Visual Studio では、高性能 IntelliSense、コード スニペット、ナビゲーション機能、書式設定、lint、リファクタリングの機能が提供されます。
ms.date: 03/13/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: eb3e3ca5d18429c60894c42bda12328836dc6fc8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "73024719"
---
# <a name="edit-python-code"></a>Python コードの編集

開発者は、開発時間の多くをコード エディターで費やすため、[Visual Studio での Python のサポート](installing-python-support-in-visual-studio.md)は、生産性を向上させる機能を提供しています。 機能には、IntelliSense 構文の強調表示、オートコンプリート、署名ヘルプ、メソッドのオーバーライド、検索、ナビゲーションが含まれます。

また、エディターは Visual Studio の**対話型**ウィンドウと統合され、この 2 つの間で簡単にコードを交換することができます。 詳細については、[「チュートリアル」の「手順 3:対話型 REPL ウィンドウを使用する」](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)と、[対話型ウィンドウの使用 - 対話型コマンドにコードを送信する](python-interactive-repl-in-visual-studio.md#send-to-interactive-command)に関するページを参照してください。

Visual Studio でのコードの編集に関する全般的な説明については、「[コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)」をご覧ください。 また、コードの特定のセクションに注意を集中するのに役立つ、[アウトライン](../ide/outlining.md)についての記事もご覧ください。

また、各モジュールで定義されている Python クラスとそれらのクラスで定義されている関数を調べるために、Visual Studio **オブジェクト ブラウザー**を使うことができます ( **[表示]**  >  **[その他のウィンドウ]**  >  **[オブジェクト ブラウザー]** の順に選択するか、**Ctrl**+**W** > **J** キーを押す)。

## <a name="intellisense"></a>IntelliSense

IntelliSense により、[入力候補](#completions)、[シグネチャ ヘルプ](#signature-help)、[クイック ヒント](#quick-info)、[コードの色分け表示](#code-coloring)が提供されます。 Visual Studio 2017 バージョン 15.7 以降では、[型ヒント](#type-hints)もサポートされています。

パフォーマンスを向上するために、Visual Studio 2017 バージョン 15.5 以前の IntelliSense は、プロジェクト内の各 Python 環境用に生成される入力候補データベースに依存しています。 パッケージを追加、削除、更新した場合はデータベースの更新が必要になる可能性があります。 データベースの状態は、**[IntelliSense]** タブの **[Python 環境]** ウィンドウ (**ソリューション エクスプローラー**の兄弟ウィンドウ) に表示されます (「[環境ウィンドウ リファレンス](python-environments-window-tab-reference.md)」を参照)。

Visual Studio 2017 バージョン 15.6 以降では、別の手段を使用して、データベースに依存しない IntelliSense 入力候補が提供されています。

### <a name="completions"></a>入力候補

入力候補は、エディター内の現在の場所に入力するのに適している可能性があるステートメント、識別子、その他の単語として表示されます。 一覧に表示される項目はコンテキストに基づいており、誤った選択肢や不適切な選択肢を除くようにフィルター処理されています。 入力候補は別のステートメント (`import` など) や演算子 (ピリオドを含む) を入力したときによく表示されますが、**Ctrl**+**J** > **Space** キーを押すことでいつでも表示できます。

![Visual Studio エディターのメンバー入力候補](media/code-editing-completions-simple.png)

入力候補一覧が開いたら、方向キーまたはマウスを使用するか、入力を続けることによって目的の入力候補を検索できます。 多くの文字を入力するほど一覧が絞り込まれ、可能性の高い入力候補が表示されます。 次のようなショートカットも使用できます。

- 名前の先頭ではない文字を入力する ('parse' を入力して 'argparse' を検索するなど)
- 単語の先頭の数文字のみを入力する ('abc' を入力して 'AbstractBaseClass' を検索する、'air' を入力して 'as_integer_ratio' を検索するなど)
- 文字をスキップする ('b64' を入力して 'base64' を検索するなど)

以下に、いくつかの例を示します。

![Visual Studio エディターのメンバー入力候補とフィルタリング](media/code-editing-completion-filtering.png)

変数または値の後にピリオドを入力するとメンバー入力候補が自動的に表示され、可能性がある型のメソッドと属性が表示されます。 複数の型の可能性がある変数の場合は、すべての型のすべての候補が一覧に表示され、各入力候補がどの型でサポートされるかを示した追加情報も表示されます。 入力候補がすべての型でサポートされる場合は、注釈なしで表示されます。

![Visual Studio エディターのメンバー入力候補と複数の型](media/code-editing-completion-types.png)

既定では、"dunder" メンバー (先頭および末尾にダブル アンダースコアが付いたメンバー) は表示されません。 一般に、このようなメンバーに直接アクセスしてはいけません。 しかし、必要な場合は、先頭に二重アンダー スコアを入力すると、これらの入力候補が一覧に追加されます。

![Visual Studio エディターのプライベートのメンバー入力候補](media/code-editing-completion-dunder.png)

`import` および `from ... import` ステートメントでは、インポートできるモジュールの一覧が表示されます。 `from ... import` を使用すると、一覧には指定したモジュールからインポートできるメンバーが含まれています。

![Visual Studio エディターのインポートの入力候補](media/code-editing-completion-import.png)

`raise` および `except` ステートメントでは、エラーの種類として可能性があるクラスの一覧が表示されます。 この一覧にはすべてのユーザー定義例外は含まれていない可能性がありますが、入力に適した組み込みの例外をすばやく見つけるのに役立ちます。

![Visual Studio エディターの例外の入力候補](media/code-editing-completion-exception.png)

@ を入力するとデコレーターが開始され、可能性があるデコレーターが表示されます。 これらの項目の多くはデコレーターとして使用できないため、ライブラリのドキュメントを確認して、どれを使用するかを判断する必要があります。

![Visual Studio エディターのデコレーターの入力候補](media/code-editing-completion-decorator.png)

> [!Tip]
> 入力候補の動作は、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[Python]**  >  **[詳細設定]** で構成できます。 この設定の **[検索文字列に基づいてリストをフィルターする]** では、入力の際に入力候補がフィルター処理されます (既定ではオンになっています)。また、 **[メンバーの入力候補にメンバーの共通部分を表示する]** では、可能性のあるすべての型でサポートされている入力候補のみが表示されます (既定ではオフになっています)。 「[Options - completion results](python-support-options-and-settings-in-visual-studio.md#completion-results)」(オプション - メンバー入力候補の結果) を参照してください。

### <a name="type-hints"></a>型ヒント

*Visual Studio 2017 バージョン 15.7 以降。*

Python 3.5 以降の "型ヒント" ([PEP 484](https://www.python.org/dev/peps/pep-0484/) (python.org) とは、引数、戻り値、およびクラス属性の型を示す関数およびクラスの注釈構文です。 IntelliSense では、そのような注釈がある関数呼び出し、引数、および変数上にマウス カーソルを置くと、型ヒントが表示されます。

次の例では、`Vector` クラスが `List[float]` と宣言されており、`scale` 関数にはその引数と戻り値の両方の型ヒントが含まれています。 その関数呼び出しの上にマウス カーソルを置くと、型ヒントが表示されます。

![型ヒントを表示するために関数呼び出しの上にマウスを置く](media/code-editing-type-hints1.png)

次の例では、IntelliSense 入力候補のポップアップで `Employee` クラスの注釈付きの属性がどのように表示されるか示しています。

![型ヒントを示す IntelliSense の入力候補](media/code-editing-type-hints2.png)

エラーは通常実行時まで表示されないため、プロジェクト全体の型ヒントを検証すると役立ちます。 このために、Visual Studio では、**ソリューション エクスプローラー**の **[Python]** > **[Mypy の実行]** のコンテキスト メニュー コマンドを通じて、業界標準の MyPy ツールが統合されています。

![ソリューション エクスプローラーで MyPy コンテキスト メニュー コマンドを実行する](media/code-editing-type-hints-run-mypy.png)

コマンドを実行すると、必要に応じて mypy パッケージのインストールが求められます。 すると、Visual Studio では mypy が実行され、プロジェクトのすべての Python ファイルで型ヒントが検証されます。 エラーは Visual Studio の **[エラー一覧]** ウィンドウに表示されます。 ウィンドウでアイテムを選択すると、コードの適切な行に移動します。

単純な例として、次の関数定義には、`input` 引数は `str` 型であることを示す型ヒントが含まれています。それに対し、その関数呼び出しは引数を渡そうとします。

```python
def commas_to_colons(input: str):
    items = input.split(',')
    items = [x.strip() for x in items]
    return ':'.join(items)

commas_to_colons(1)
```

このコードで **[Mypy の実行]** コマンドを使用すると、次のエラーが生成されます。

![型ヒントを検証する mypy の結果例](media/code-editing-type-hints-validation-error.png)

::: moniker range="vs-2017"
> [!Tip]
> バージョン 3.5 より前の Python の場合、Visual Studio では、Typeshed "*スタブ ファイル*" ( *.pyi*) を使用して提供される型ヒントも表示されます。 スタブ ファイルは、コードに直接型ヒントを含めたくない場合や、型ヒントを直接使用しないライブラリ用に型ヒントを作成する場合に使用します。 詳細については、mypy プロジェクト wiki で「[Create Stubs for Python Modules](https://github.com/python/mypy/wiki/Creating-Stubs-For-Python-Modules)」 (Python モジュール用のスタブを作成する) を参照してください。
>
> 現時点では、Visual Studio ではコメントの型ヒントはサポートされていません。
::: moniker-end
::: moniker range=">=vs-2019"
> [!Tip]
> バージョン 3.5 より前の Python の場合、Visual Studio では、Typeshed "*スタブ ファイル*" ( *.pyi*) を使用して提供される型ヒントも表示されます。 スタブ ファイルは、コードに直接型ヒントを含めたくない場合や、型ヒントを直接使用しないライブラリ用に型ヒントを作成する場合に使用します。 詳細については、mypy プロジェクト wiki で「[Create Stubs for Python Modules](https://github.com/python/mypy/wiki/Creating-Stubs-For-Python-Modules)」 (Python モジュール用のスタブを作成する) を参照してください。
>
> Visual Studio には、Python 2 および 3 用の Typeshed ファイルのバンドル セットが含まれているので、追加のダウンロードは必要ありません。 ただし、異なるファイルのセットを使いたい場合は、 **[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[言語サーバー]** オプションでパスを指定できます。 [言語サーバーのオプション](python-support-options-and-settings-in-visual-studio.md#language-server-options)に関する記事をご覧ください。
>
> 現時点では、Visual Studio ではコメントの型ヒントはサポートされていません。
::: moniker-end

### <a name="signature-help"></a>シグネチャ ヘルプ

関数を呼び出すコードの作成中に始め `(` を入力するとシグネチャ ヘルプが表示され、利用できるドキュメントとパラメーター情報が表示されます。 これは関数呼び出し内で **Ctrl**+**Shift**+**Space** キーを押して表示することもできます。 表示される情報は関数のソース コード内のドキュメント文字列によって異なりますが、すべての既定値が含まれます。

![Visual Studio エディターのシグネチャ ヘルプ](media/code-editing-signature-help.png)

> [!Tip]
> シグネチャ ヘルプを無効にするには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[Python]**  >  **[全般]** に移動し、 **[ステートメント入力候補]**  >  **[パラメーター情報]** をオフにします。

### <a name="quick-info"></a>クイック ヒント

識別子にマウス ポインターを置くと、クイック ヒントが表示されます。 クイック ヒントには、識別子に応じて、可能性のある値または型、利用できるドキュメント、戻り値の型、定義の場所が表示されます。

![Visual Studio エディターのクイック ヒント](media/code-editing-quick-info.png)

### <a name="code-coloring"></a>コードの色分け表示

コードの色分け表示では、コード分析の情報を使用して、変数、ステートメント、その他のコード部分を色分けして示します。 たとえば、モジュールまたはクラスを参照する変数を関数やその他の値とは異なる色で表示したり、パラメーター名をローカル変数やグローバル変数とは異なる色で表示したりできます (既定では、関数は太字では表示されません)。

![Visual Studio エディターのコードと構文の色分け表示](media/code-editing-code-coloring.png)

色をカスタマイズするには、**[ツール]** > **[オプション]** > **[環境]** > **[フォントおよび色]** に移動し、**[表示アイテム]** の一覧で **Python** のエントリを変更します。

![Visual Studio のフォント オプションと色オプション](media/code-editing-customize-colors.png)

> [!Tip]
> コードの色分け表示を無効にするには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[Python]**  >  **[詳細設定]** に移動し、 **[その他のオプション]**  >  **[Color names based on type]\(種類に基づく色の名前\)** をオフにします。 「[Options - Miscellaneous Options](python-support-options-and-settings-in-visual-studio.md#miscellaneous-options)」(オプション ∸ その他のオプション) を参照してください。

## <a name="code-snippets"></a>コード スニペット

コード スニペットはファイルに挿入できるコード フラグメントであり、ショートカットを入力して **Tab** キーを押すか、 **[編集]**  >  **[IntelliSense]**  >  **[コード スニペットの挿入]** と **[ブロックの挿入]** コマンドを使用して **[Python]** を選び、目的のスニペットを選択することで、ファイルに挿入できます。

たとえば、`class` は、クラス定義を挿入するコード スニペットのショートカットです。 `class` を入力すると、そのスニペットが自動入力候補一覧に表示されます。

![class ショートカットに対応するコード スニペット](media/code-editing-code-snippet-class.png)

**Tab** キーを押すと、クラスの残りの部分が生成されます。 強調表示されたフィールド間を **Tab** キーで移動して名前と基底クラスの一覧を上書きし、**Enter** キーを押して本文の入力を開始できます。

![補完するコード スニペットの領域の強調表示](media/code-editing-code-snippets.png)

### <a name="menu-commands"></a>メニュー コマンド

**[編集]**  >  **[IntelliSense]**  >  **[コード スニペットの挿入]** メニュー コマンドを使用する場合は、次のように、まず、 **[Python]** を選択してからスニペットを選びます。

![[コード スニペットの挿入] コマンドによるコード スニペットの選択](media/code-editing-code-snippet-insert.png)

**[編集]**  >  **[IntelliSense]**  >  **[ブロックの挿入]** コマンドも、テキスト エディター内の現在の選択範囲を、選択済みの構造体の要素内に配置します。 たとえば、次のようなコードがあるとします。

```python
sum = 0
for x in range(1, 100):
    sum = sum + x
```

このコードを選択し、 **[ブロックの挿入]** コマンドを選択すると、使用可能なスニペットの一覧が表示されます。 一覧から **def** を選択すると、選択済みのコードが関数定義内に配置され、強調表示されている関数の名前と引数の間を **Tab** キーを使用して移動できます。

![コード スニペットに対する [ブロックの挿入] コマンドの使用](media/code-editing-code-snippet-surround-with.png)

### <a name="examine-available-snippets"></a>利用可能なスニペットを調べる

利用可能なコード スニペットは、**コード スニペット マネージャー**で確認できます。これを開くには、 **[ツール]**  >  **[コード スニペット マネージャー]** メニュー コマンドを使用し、言語として **[Python]** を選択します。

![Visual Studio のコード スニペット マネージャー](media/code-editing-code-snippets-manager.png)

独自のスニペットを作成する場合は、「[チュートリアル:コード スニペットを作成する](../ide/walkthrough-creating-a-code-snippet.md)」を参照してください。

便利なコード スニペットを作成したので共有したいとお考えの場合は、ぜひ gist に投稿して[マイクロソフトまでお知らせください](https://github.com/Microsoft/PTVS/issues)。 Visual Studio の将来のリリースに含めさせていただく可能性があります。

## <a name="navigate-your-code"></a>コードの移動

Visual Studio の Python のサポートとして、ソース コードが提供されているライブラリを含め、[ナビゲーション バー](#navigation-bar)、[ **[定義へ移動]** ](#go-to-definition)、[ **[移動]** ](#navigate-to)、[ **[すべての参照の検索]** ](#find-all-references) など、コード内をすばやく移動するためのいくつかの手段が用意されています。 また、Visual Studio の [**オブジェクト ブラウザー**](../ide/viewing-the-structure-of-code.md#BKMK_ObjectBrowser)も使用できます。

### <a name="navigation-bar"></a>[ナビゲーション バー]

ナビゲーション バーは各エディター ウィンドウの上部に表示され、2 つのレベルの定義リストを含みます。 左側のドロップダウン リストには、現在のファイル内の最上位のクラスと関数の定義が表示されます。右側のドロップダウン リストには、左側に表示されているスコープ内の定義のリストが表示されます。 エディター内を移動すると、リストが現在のコンテキストを示すように更新され、これらのリストからエントリを選択してそのエントリに直接ジャンプすることもできます。

![Visual Studio エディターのナビゲーション バー](media/code-editing-navigation-bar.png)

> [!Tip]
> ナビゲーション バーを非表示にするには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[Python]**  >  **[全般]** に移動し、 **[設定]**  >  **[ナビゲーション バー]** をオフにします。

### <a name="go-to-definition"></a>[定義へ移動]

**[定義へ移動]** を使用すると、識別子 (関数名、クラス、変数など) の使用場所から、その識別子が定義されているソース コードにすばやくジャンプできます。 これは、識別子を右クリックして **[定義へ移動]** を選択するか、識別子にキャレットを置いて **F12** キーを押すと起動されます。 この機能は、ソース コードが利用可能ならばコードと外部ライブラリ全体で機能します。 ライブラリのソース コードを利用できない場合に **[定義へ移動]** を使用すると、モジュール参照の関連する `import` ステートメントにジャンプするか、エラーが表示されます。

![Visual Studio の [定義へ移動] コマンド](media/code-editing-go-to-definition.png)

### <a name="navigate-to"></a>移動

**[編集]**  >  **[移動]** コマンド (**Ctrl**+ **,** キー) を使用すると、エディター内に検索ボックスが表示されます。ボックスに任意の文字列を入力すると、その文字列を含む関数、クラス、変数を定義するコード内の一致候補が表示されます。 この機能は **[定義へ移動]** の機能と似ていますが、識別子の使用場所を探す必要がありません。

任意の名前をダブルクリックするか、方向キーで選択して **Enter** キーを押すと、その識別子の定義に移動します。

![Visual Studio の [移動] コマンド](media/code-editing-navigate-to.png)

### <a name="find-all-references"></a>[すべての参照の検索]

**[すべての参照の検索]** は、特定の識別子の定義場所と使用場所の両方 (インポートと代入を含む) を見つけるのに便利な方法です。 これは、識別子を右クリックして **[すべての参照の検索]** を選択するか、識別子にキャレットを置いて **Shift**+**F12** キーを押すと起動されます。 一覧内の項目をダブルクリックすると、その場所に移動します。

![[すべての参照の検索] の結果](media/code-editing-find-all-references.png)

## <a name="see-also"></a>関連項目

- [書式設定](formatting-python-code.md)
- [リファクタリング](refactoring-python-code.md)
- [リンターの使用](linting-python-code.md)
