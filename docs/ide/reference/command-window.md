---
title: コマンド ウィンドウ
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.CommandWindow
helpviewer_keywords:
- IDE, Command window
- Mark mode in Command window
- Command window
- Command mode in Command window
- IDE Command window
ms.assetid: 48711628-1909-4713-a73e-d7b714c77f8a
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75792518eadc5449f070b90f3f1e8c2da38bf2b3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748784"
---
# <a name="command-window"></a>コマンド ウィンドウ
**[コマンド]** ウィンドウは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の統合開発環境 (IDE) でコマンドやエイリアスを実行するときに使用します。 メニュー コマンドと、メニューに表示されないコマンドの両方を実行できます。 **[コマンド]** ウィンドウを表示するには、 **[表示]** メニューの **[その他のウィンドウ]** を選択し、 **[コマンド ウィンドウ]** をクリックします。

## <a name="displaying-the-values-of-variables"></a>変数の値の表示
変数 `varA` の値を確認するには、[印刷コマンド](../../ide/reference/print-command.md)を使用します。

```cmd
>Debug.Print varA
```

疑問符 (?) は`Debug.Print` のエイリアスであるため、このコマンドは次のように書き換えることもできます。

```cmd
>? varA
```

コマンドをどちらで入力した場合でも、変数 `varA` の現在の値が返されます。

## <a name="entering-commands"></a>コマンドの入力
不等号 (`>`) は改行を示す記号としてコマンド ウィンドウの左端に表示されます。 上方向キーおよび下方向キーを使用して、以前に入力したコマンドの間をスクロールします。

|タスク|ソリューション|例|
|----------|--------------|-------------|
|式を評価する。|式の先頭に疑問符 (`?`) を付けます。|`? myvar`|
|[イミディエイト] ウィンドウに切り替る。|不等号 (>) を付けずにウィンドウに「`immed`」と入力します。|`immed`|
|[イミディエイト] ウィンドウから [コマンド] ウィンドウに切り替る。|ウィンドウに「`cmd`」と入力します。|`>cmd`|

コマンド モードでの移動には、次のショートカット キーを使用できます。

|アクション|カーソルの位置|ショートカット キー|
|------------| - |----------------|
|以前に入力したコマンドを一覧内で順番に参照する。|入力行|↑キーおよび↓キー|
|ウィンドウを上にスクロールする。|コマンド ウィンドウの内容|Ctrl + ↑|
|ウィンドウを下にスクロールする。|コマンド ウィンドウの内容|↓キーまたは Ctrl + ↓キー|

> [!TIP]
> 以前に入力したコマンドの全体または一部を入力行にコピーするには、そのコマンドまでスクロールし、その全体または一部を強調表示してから Enter キーを押します。

## <a name="mark-mode"></a>マーク モード
**[コマンド]** ウィンドウで、既に出力されている任意の行をクリックすると、自動的にマーク モードに切り替わります。 これにより、テキスト エディターでの操作と同じように、既に入力されたコマンドのテキストを選択、編集、およびコピーし、現在の行に貼り付けることができます。

## <a name="the-equals--sign"></a>等号 (=)
`EvaluateStatement` コマンドをどのウィンドウに入力するかによって、等号 (=) を比較演算子として解釈するのか、代入演算子として解釈するのかが決まります。

**[コマンド]** ウィンドウの場合、等号 (=) は、比較演算子と解釈されます。 **[コマンド]** ウィンドウでは、代入演算子は使用できません。 したがって、たとえば変数 `varA` と変数 `varB` の値が異なる場合、コマンド `>Debug.EvaluateStatement(varA=varB)` は `False` の値を返します。

一方、 **[イミディエイト]** ウィンドウの場合、等号 (=) は、代入演算子と解釈されます。 たとえば、コマンド `>Debug.EvaluateStatement(varA=varB)` は変数 `varA` に変数 `varB` の値を代入します。

## <a name="parameters-switches-and-values"></a>パラメーター、スイッチ、および値
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンドには、引数、スイッチ、値を必要とするコマンドと省略できるコマンドがあります。 このようなコマンドを処理するときは、いくつかの規則が適用されます。 リッチ コマンドの例を次に示し、用語について説明します。

```cmd
Edit.ReplaceInFiles /case /pattern:regex var[1-3]+ oldpar
```

この例の用語の意味は次のとおりです。

- `Edit.ReplaceInFiles` はコマンドです。

- `/case` と `/pattern:regex` はスイッチです (前にスラッシュ (/) を付けます)。

- `regex` は `/pattern` スイッチの値です。`/case` スイッチには値がありません。

- `var[1-3]+` と `oldpar` はパラメーターです。

    > [!NOTE]
    > コマンド、パラメーター、スイッチ、または値にスペースが含まれる場合は、二重引用符 (") で囲む必要があります。

スイッチとパラメーターの位置は、コマンド ライン上で自由に入れ替えることができます。例外として、[Shell](../../ide/reference/shell-command.md) コマンドの場合は、スイッチとパラメーターを特定の順序に指定する必要があります。

コマンドでサポートされるほとんどすべてのスイッチには、短い形式 (1 文字) と長い形式の 2 とおりの形式があります。 複数の短い形式のスイッチは、結合して 1 つのグループにまとめることができます。 たとえば、`/p /g /m` をまとめて `/pgm` と表現できます。

複数の短い形式のスイッチがグループ化され、値が指定された場合、その値はすべてのスイッチに適用されます。 たとえば、`/pgm:123` は `/p:123 /g:123 /m:123` と同等です。 グループ内のいずれかのスイッチが値を受け付けない場合は、エラーになります。

## <a name="escape-characters"></a>エスケープ文字
コマンド ラインにカレット (^) 文字があると、その直後の文字は制御文字としてではなくリテラル文字として解釈されます。 したがって、引用符 (")、スペース、先頭のスラッシュ、カレット、その他の任意のリテラル文字をパラメーターまたはスイッチの値に直接埋め込むことができます。ただし、スイッチ名には埋め込むことができません。 たとえば、オブジェクトに適用された

```cmd
>Edit.Find ^^t /regex
```

カレットは、引用符の前後のどちらに置かれた場合でも同じ働きをします。 行の最後の文字がカレットの場合は無視されます。 ここに示した例では、"^t" というパターンを検索する方法を示しています。

## <a name="use-quotes-for-path-names-with-spaces"></a>スペースを含むパス名には引用符を使用する
たとえば、スペースを含むパスを持つファイルを開く場合は、スペースを含むパスまたはパス セグメントを二重引用符で囲む必要があります (**C:\\"Program Files"** または **"C:\Program Files"** )。

## <a name="see-also"></a>関連項目

- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
