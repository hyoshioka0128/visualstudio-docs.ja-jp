---
title: Python コードの書式を設定する
description: Visual Studio では、間隔、ステートメント、折り返し、コメントなど、Python コードの書式を自動的に再設定できます。
ms.date: 03/13/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 6e95d05c3fbc0dd46d235c7480bd4a9caa48947e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62957537"
---
# <a name="format-python-code"></a>Python コードの書式を設定する

Visual Studio を使用すると、事前に構成した書式設定オプションに合わせて、すばやくコードの書式を再設定できます。

- 選択範囲の書式を設定するには、 **[編集]**  >  **[詳細設定]**  >  **[選択範囲のフォーマット]** を選択するか、**Ctrl**+**E** > **F** キーを押します。
- ファイル全体の書式を設定するには、 **[編集]**  >  **[詳細設定]**  >  **[ドキュメントのフォーマット]** を選択するか、**Ctrl**+**E** > **D** キーを押します。

オプションは、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[Python]**  >  **[書式設定]** およびその入れ子のタブを使用して設定します。 これらのオプションを表示するには、 **[すべての設定を表示]** を選択する必要があります。

![Visual Studio の Python の [書式設定] オプション](media/options-editor-formatting.png)

[書式設定] オプションは、既定で [PEP 8 スタイル ガイド](https://www.python.org/dev/peps/pep-0008/)のスーパーセットと一致するように設定されています。 **[全般]** タブでは、どのような場合に書式設定を適用するかを指定します。この記事では、他の 3 つのタブについて説明します。

[Visual Studio の Python のサポート](installing-python-support-in-visual-studio.md)で、 **[編集]**  >  **[詳細設定]** メニューに [ **[コメントを段落幅に合わせる]** ](#fill-comment-paragraph-command) という便利なコマンドも追加されています。これについても後で説明します。

## <a name="spacing"></a>スペース

**[スペース]** では、さまざまな言語コンストラクトの前後のスペースを挿入するか削除するかを指定します。 各オプションで指定できる値は次の 3 つです。

- オン: スペースを挿入します。
- オフ: スペースを削除します。
- 不確定: 元の書式設定のままにします。

さまざまなオプションの例を以下の表に示します。

| クラス定義のオプション | チェック済み | オフにした場合 |
| --- | --- | --- |
| **Insert space between a class declaration's name and bases list \(クラス宣言の名前と基底クラス リストの間に空白を挿入する\)** | `class X (object): pass` | `class X(object): pass` |
| **基本リストのかっこ内に空白を挿入する** | `class X( object ): pass` | `class X(object): pass` |
| **空の基本リストのかっこ内に空白を挿入する** | `class X( ): pass` | `class X(): pass` |

<br/>

| 関数定義のオプション | チェック済み | オフにした場合 |
| --- | --- | --- |
| **Insert space between a function declaration's name and parameter list \(関数宣言の名前とパラメーター リストの間に空白を挿入する\)** | `def X (): pass` | `def X(): pass` |
| **パラメーター リストのかっこ内にスペースを挿入する** | `def X( a, b ): pass` | `def X(a, b): pass` |
| **空のパラメーター リストのかっこ内にスペースを挿入する** | `def X( ): pass` | `def X(): pass` |
| **Insert spaces around '=' in default parameter values \(既定のパラメーター値の '=' の前後にスペースを挿入する\)** | `includes X(a = 42): pass` | `includes X(a=42): pass` |
| **Insert space before and after return annotation operators \(リターン注釈演算子の前後にスペースを挿入する\)** | `includes X() -> 42: pass` | `includes X()->42: pass` |

<br/>

| 演算子のオプション | チェック済み | オフにした場合 |
| --- | --- | --- |
| **バイナリ演算子の前後に空白を挿入する** | `a + b` | `a+b` |
| **代入の前後に空白を挿入する** | `a = b` | `a=b` |

<br/>

| 式のスペースのオプション | チェック済み | オフにした場合 |
| --- | --- | --- |
| **Insert space between a function call's name and argument list \(関数呼び出しの名前と引数リストの間にスペースを挿入する\)** | `X ()` | `X()` |
| **空の引数リストのかっこ内にスペースを挿入する** | `X( )` | `X()` |
| **引数リストのかっこ内にスペースを挿入する** | `X( a, b )` | `X(a, b)` |
| **Insert space within parentheses of expression \(式のかっこ内にスペースを挿入する\)** | `( a )` | `(a)` |
| **Insert space within empty tuple parentheses \(空のタプルのかっこ内にスペースを挿入する\)** | `( )` | `()` |
| **タプルのかっこの内側に空白を挿入する** | `( a, b )` | `(a, b)` |
| **空の角かっこ内にスペースを挿入する** | `[ ]` | `[]` |
| **Insert spaces within square brackets of lists \(リストの角かっこ内にスペースを挿入する\)** | `[ a, b ]` | `[a, b]` |
| **Insert space before open square bracket \(開始角かっこの前にスペースを挿入する\)** | `x [i]` | `x[i]` |
| **角かっこ内にスペースを挿入する** | `x[ i ]` | `x[i]` |

<br/>

## <a name="statements"></a>ステートメント

**[ステートメント]** オプションでは、さまざまなステートメントをより Python らしい形式に自動的に書き換えるかどうかを指定します。

| オプション | 書式設定前 | 書式設定後 |
| --- | --- | --- |
| **Place imported modules on new line \(インポートされたモジュールを新しい行に配置する\)** | `import sys, pickle` | `import sys`<br/>`import pickle` |
| **不要なセミコロンを削除する** | `x = 42;` | `x = 42` |
| **Place multiple statements on new lines \(複数のステートメントを新しい行に配置する\)** | `x = 42; y = 100` | `x = 42`<br/>`y = 100` |

## <a name="wrapping"></a>折り返し

**[折り返し]** では、 **[コメントの最大幅]** (既定値は 80) を設定できます。 **[長すぎるコメントを折り返します]** オプションを設定した場合、その最大幅を超えるコメントは自動的に再フォーマットされます。

```python
# Wrapped to 40 columns
# There should be one-- and preferably
# only one --obvious way to do it.
```

```python
# Not-wrapped:
# There should be one-- and preferably only one --obvious way to do it.
```

## <a name="fill-comment-paragraph-command"></a>[Fill Comment Paragraph(コメント段落をページ幅に合わせる)] コマンド

**[編集]**  >  **[詳細設定]**  >  **[コメントを段落幅に合わせる]** (**Ctrl**+**E** > **P**) を使用すると、コメント テキストがリフローおよび書式設定され、複数の短い行を 1 行にまとめたり、長い行を複数の行に分けたりできます。

次に例を示します。

```python
# foo
# bar
# baz
```

変更後:

```python
# foo bar baz
```

```python
# This is a very long long long long long long long long long long long long long long long long long long long comment
```

変更後:

```python
# This is a very long long long long long long long long long long long long
# long long long long long long long comment
```
