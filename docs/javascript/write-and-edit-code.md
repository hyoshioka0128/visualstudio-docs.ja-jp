---
title: JavaScript 開発者向けの編集の概要
description: この Visual Studio のコード エディターの概要では、Visual Studio で JavaScript コードを記述、コード内を移動、およびコードを理解する簡単な方法をいくつか示します。
ms.date: 12/13/2018
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: f48e7a8be8d902a487ae4f7fdac9e6d85f7b5517
ms.sourcegitcommit: b8ec700fc4c14c68c6ce280f29c19870261990d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87453757"
---
# <a name="learn-to-use-the-code-editor"></a>コード エディターを使用方法について学習する

この Visual Studio のコード エディターの概要では、Visual Studio でコードを記述、コード内を移動、およびコードを理解する簡単な方法をいくつか示します。

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。 実行するアプリ開発の種類によっては、Visual Studio と共に **Node.js ワークロード**をインストールする必要がある場合があります。 TypeScript の言語サービスを取得する方法の詳細については、「[TypeScript のサポート](../javascript/javascript-in-vs-2019.md#typescript-support)」をご覧ください。

この記事では、既に JavaScript の開発に慣れていることを前提としています。 慣れていない場合は、最初に [Node.js と Express のアプリの作成](../javascript/tutorial-nodejs.md)などのチュートリアルに関するページを参照することをお勧めします。

## <a name="add-a-new-project-file"></a>新しいプロジェクト ファイルを追加する

IDE を使用して、新しいファイルをプロジェクトに追加することができます。

1. Visual Studio でプロジェクトを開いた状態で、ソリューション エクスプローラー (右側のウィンドウ) でフォルダーまたはプロジェクト ノードを右クリックし、 **[追加]**  >  **[新しい項目]** の順に選択します。

1. **[新しいファイル]** ダイアログ ボックスの **[全般]** カテゴリで、 **[JavaScript ファイル]** など、追加するファイルの種類を選んでから、 **[開く]** を選択します。

    新しいファイルがプロジェクトに追加され、エディターで開かれます。

## <a name="use-intellisense-to-complete-words"></a>IntelliSense を使用した入力補完

コードを記述する場合、IntelliSense は貴重なリソースです。 このリソースでは、使用可能な型のメンバーに関する情報、またはメソッドの各種オーバーロードのためのパラメーターの詳細を表示できます。 次のコードで、「`Router()`」と入力すると、渡すことができる引数の種類が示されます。 これはシグネチャ ヘルプと呼ばれます。

![IntelliSense を使用する](../javascript/media/write-code-signature-checking.png)

また、IntelliSense を使用すると、単語を区別するために十分な文字を入力した後に入力補完を利用することができます。 次のコードで `data` 文字列の後ろにカーソルを置き、「`get`」と入力すると、IntelliSense で、コードで前に定義した関数、またはプロジェクトに追加したサードパーティ ライブラリで定義した関数が表示されます。

![IntelliSense を使用する](../javascript/media/write-code-intellisense.png)

また、IntelliSense では、プログラミング要素をポイントしたときに種類に関する情報を表示できます。

IntelliSense 情報を提供する場合、言語サービスで TypeScript *d.ts* ファイルと JSDoc コメントを使用できます。 最も一般的な JavaScript ライブラリの場合、*d.ts* ファイルは自動的に取得されます。 IntelliSense 情報の取得方法について詳しくは、「[JavaScript IntelliSense](../ide/javascript-intellisense.md?toc=/visualstudio/javascript/toc.json)」を参照してください

## <a name="check-syntax"></a>構文の確認

言語サービスでは ESLint を使用して、構文チェックと lint 処理を行います。 エディターで構文チェックのオプションを設定する必要がある場合は、 **[ツール]**  >  **[オプション]**  >  **[JavaScript/TypeScript]**  >  **[Lint]** の順に選択します。 lint オプションでは、グローバルな ESLint 構成ファイルが示されます。

次のコードでは、式の構文が緑色 (緑の波線) で強調表示されています。 構文の強調表示にカーソルを合わせます。

![構文エラーの表示](../javascript/media/write-code-syntax-checking.png)

このメッセージの最後の行から、言語サービスでコンマ (`,`) が要求されていることがわかります。 緑の波線は警告を示します。 赤の波線はエラーを示します。

下のウィンドウで、 **[エラー一覧]** タブをクリックすることで、ファイル名と行番号と共に警告と説明を表示できます。

![エラー一覧の表示](../javascript/media/write-code-error-list.png)

`"data"` の前にコンマ (`,`) を追加することで、このコードを修正できます。

リンティングの詳細については、「[リンティング](https://github.com/microsoft/JSTSdocs/blob/master/articles/editor/linting.md)」をご覧ください。

## <a name="comment-out-code"></a>コメント アウト コード

ツールバー (Visual Studio のメニュー バーの下にあるボタンの列) は、コード作成時の生産性を高めるのに役立ちます。 たとえば、IntelliSense 補完モードの切り替え (特に、[IntelliSense](../ide/using-intellisense.md) は、一致するメソッドの一覧を表示するコーディング支援機能)、行のインデントの増減、またはコンパイルしたくないコードをコメント アウトを行うことができます。 このセクションでは、一部のコードをコメント アウトします。

エディターで 1 行以上のコードを選択し、ツール バーの **[選択された行をコメントアウトします。]** ボタン ![コメント アウト ボタン](../javascript/media/write-code-comment-out.png) を選びます。 キーボードを使用する場合は、**Ctrl**+**K** キー、**Ctrl**+**C** キーを押します。

選択した各行の先頭に JavaScript コメント文字 `//` を追加すると、コードがコメント アウトされます。

## <a name="collapse-code-blocks"></a>コード ブロックを折りたたむ

コードの一部の領域のビューを整理する必要がある場合は、折りたたむことができます。 関数の最初の行の余白にある、内部にマイナス記号が示された小さな灰色のボックスを選択します。 または、キーボードを使用している場合は、コンストラクター コード内の任意の場所にカーソルを置き、**Ctrl**+**M** キー、**Ctrl**+**M** キーを押します。

![アウトライン折りたたみボタン](../javascript/media/write-code-collapse-code.png)

コード ブロックが最初の行に折りたたまれ、後続に省略記号 (`...`) が表示されます。 コード ブロックを再度展開するには、現在内部にプラス記号が表示されている同じ灰色のボックスをクリックするか、**Ctrl**+**M** キー、**Ctrl**+**M** キーをもう一度押します。 これは、[アウトライン](../ide/outlining.md)機能と呼ばれ、長い関数やクラス全体を折りたたむ場合に特に便利です。

## <a name="view-definitions"></a>定義の表示

Visual Studio エディターでは、型や関数などの定義の検査を容易に行うことができます。1 つの方法として、たとえば、プログラミング要素が参照されている任意の場所で **[定義へ移動]** を選択して、定義を含むファイルに移動します。 作業中のファイルからフォーカスを移動しないより迅速な方法としては、[[定義をここに表示]](../ide/go-to-and-peek-definition.md#peek-definition) を使用します。 以下の例で `render` メソッドの定義を表示してみましょう。

`render` を右クリックし、コンテンツ メニューから **[定義をここに表示]** を選択します。 または、**Alt**+**F12** キーを押します。

   `render` メソッドの定義を含むポップアップ ウィンドウが表示されます。 ポップアップ ウィンドウ内をスクロールすることも、参照しているコードから別の種類の定義を参照することもできます。

   ![コード定義ウィンドウ](../javascript/media/write-code-peek-definition.png)

表示された定義ウィンドウを閉じるには、ポップアップ ウィンドウの右上にある、内部に "x" が表示された小さなボックスを選択します。

## <a name="use-code-snippets"></a>コード スニペットを使用する

Visual Studio で提供されている便利な*コード スニペット*を使用すると、一般的に使用されるコード ブロックを迅速かつ簡単に生成することができます。 [コード スニペット](../ide/code-snippets.md)は、JavaScript を含むさまざまなプログラミング言語で使用することができます。 コード ファイルに `for` ループを追加してみましょう。

スニペットを挿入する場所にカーソルを置き、右クリックして **[スニペット]**  >  **[スニペットの挿入]** の順に選択します。

![Visual Studio のコード スニペット](../javascript/media/write-code-insert-snippet.png)

エディターに **[スニペットの挿入]** ボックスが表示されます。 **[全般]** を選択し、一覧で **[for]** 項目をダブルクリックします。

![Visual Studio の for ループ用のコード スニペット](../javascript/media/write-code-insert-snippet-for-loop.png)

これで、コードに `for` ループ スニペットが追加されます。

```javascript
for (var i = 0; i < length; i++) {

}
```

目的の言語で使用可能なコード スニペットを確認するには、 **[編集]**  >  **[IntelliSense]**  >  **[スニペットの挿入]** の順に選択し、言語のフォルダーを選択します。

## <a name="see-also"></a>関連項目

- [コード スニペット](../ide/code-snippets.md)
- [コード間の移動](../ide/navigating-code.md)
- [アウトライン](../ide/outlining.md)
- [[定義へ移動] と [定義をここに表示]](../ide/go-to-and-peek-definition.md)
- [リファクタリング](../ide/refactoring-in-visual-studio.md)
- [IntelliSense を使用する](../ide/using-intellisense.md)
