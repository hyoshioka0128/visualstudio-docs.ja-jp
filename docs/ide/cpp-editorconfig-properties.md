---
title: C++ EditorConfig の書式規則
titleSuffix: ''
description: EditorConfig を使用して Visual Studio で C++ コードを書式設定する方法について説明します。
ms.date: 9/14/2020
author: jureid
ms.author: jureid
manager: jmartens
dev_langs:
- CPP
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: reference
ms.workload:
- cplusplus
monikerRange: vs-2019
ms.openlocfilehash: 490a7b29d6e3d8a2dc63c27b9e9d7226b5d22662
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970882"
---
# <a name="c-editorconfig-formatting-conventions"></a>C++ EditorConfig の書式規則

Visual Studio C++ フォーマッタには、グローバルに適用できる構成可能な設定の豊富なセットが用意されています。 特定のワークスペースの C++ 書式設定を設定するには、[clangformat](https://clang.llvm.org/docs/ClangFormat.html) または [EditorConfig](https://editorconfig.org/) を使用します。 Visual Studio と Visual Studio Code にはどちらも、グローバルの Visual Studio C++ 書式設定のそれぞれに対する EditorConfig サポートが組み込まれており、EditorConfig 設定が優先されます。 これは、EditorConfig ファイルをワークスペースに追加すると、C++ 書式設定をより細かなレベルで構成し、プロジェクトに参加するすべてのユーザーに一貫したコード スタイルを適用できることを意味します。

## <a name="c-formatting-conventions"></a>C++ 書式設定の規則

C++ 書式設定の EditorConfig 設定には、プレフィックスとして `cpp_` が付きます。 EditorConfig ファイルの例を次に示します。

```ini
[*.{c++,cc,cpp,cxx,h,h++,hh,hpp,hxx,inl,ipp,tlh,tli}]

cpp_indent_case_contents_when_block = true
cpp_new_line_before_open_brace_namespace = same_line
```

このドキュメントの残りの部分では、Visual Studio と VS Code でサポートされているすべての EditorConfig C++ 書式設定を一覧に示します。

### <a name="indentation-settings"></a>インデントの設定

**中かっこのインデント**

- 名前: `cpp_indent_braces`
- 値: `true`、`false`

**以下を基準に各行をインデントする**

- 名前: `cpp_indent_multi_line_relative_to`
- 値:
  - `outermost_parenthesis` - 新しい行を入力すると、外側の始めかっこを基準にインデントされます。
  - `innermost_parenthesis` - 新しい行を入力すると、内側の始めかっこを基準にインデントされます。
  - `statement_begin` - 新しい行を入力すると、現在のステートメントの先頭を基準にインデントされます。

**かっこ内で、入力した新しい行を揃える**

- 名前: `cpp_indent_within_parentheses`
- 値:
  - `align_to_parenthesis` - 始めかっこに内容を揃える。
  - `indent` - 新しい行をインデント。

**既存のコードで、かっこ内で改行を揃える設定を使用しない**

- 名前: `cpp_indent_preserve_within_parentheses`
- 値: `true`、`false`

**case の内容をインデントする**

- 名前: `cpp_indent_case_contents`
- 値: `true`、`false`

**case ラベルをインデントする**

- 名前: `cpp_indent_case_labels`
- 値: `true`、`false`

**case ステートメントの後に中かっこをインデントする**

- 名前: `cpp_indent_case_contents_when_block`
- 値: `true`、`false`

**パラメーターとして使うラムダの中かっこをインデントする**

- 名前: `cpp_indent_lambda_braces_when_parameter`
- 値: `true`、`false`

**goto ラベルの位置**

- 名前: `cpp_indent_goto_labels`
- 値:
  - `one_left` - 左に 1 インデント
  - `leftmost_column` - 左端の列に移動する
  - `none` - インデントされたままにする

**プリプロセッサ ディレクティブの位置**

- 名前: `cpp_indent_preprocessor`
- 値:
  - `one_left` - 左に 1 インデント
  - `leftmost_column` - 左端の列に移動する
  - `none` - インデントされたままにする

**アクセス指定子のインデント**

- 名前: `cpp_indent_access_specifiers`
- 値: `true`、`false`

**名前空間の内容をインデントする**

- 名前: `cpp_indent_namespace_contents`
- 値: `true`、`false`

**コメントのインデントを維持する**

- 名前: `cpp_indent_preserve_comments`
- 値: `true`、`false`

### <a name="newline-settings"></a>改行の設定

**名前空間の始めかっこの位置**

- 名前: `cpp_new_line_before_open_brace_namespace`
- 値:
  - `new_line` - 新しい行へ移動
  - `same_line` - 同じ行に残し、その前にスペースを 1 つ追加
  - `ignore` - 自動再配置しない

**型の始めかっこの位置**

- 名前: `cpp_new_line_before_open_brace_type`
- 値:
  - `new_line` - 新しい行へ移動
  - `same_line` - 同じ行に残し、その前にスペースを 1 つ追加
  - `ignore` - 自動再配置しない

**関数の始めかっこの位置**

- 名前: `cpp_new_line_before_open_brace_function`
- 値:
  - `new_line` - 新しい行へ移動
  - `same_line` - 同じ行に残し、その前にスペースを 1 つ追加
  - `ignore` - 自動再配置しない

**コントロール ブロックの始めかっこの位置**

- 名前: `cpp_new_line_before_open_brace_block`
- 値:
  - `new_line` - 新しい行へ移動
  - `same_line` - 同じ行に残し、その前にスペースを 1 つ追加
  - `ignore` - 自動再配置しない

**ラムダの始めかっこの位置**

- 名前: `cpp_new_line_before_open_brace_lambda`
- 値:
  - `new_line` - 新しい行へ移動
  - `same_line` - 同じ行に残し、その前にスペースを 1 つ追加
  - `ignore` - 自動再配置しない
 
**スコープの中かっこを別の行に配置する**

- 名前: `cpp_new_line_scope_braces_on_separate_lines`
- 値: `true`、`false`

**型が空の場合は、終わりかっこを始めかっこと同じ行に移動する**

- 名前: `cpp_new_line_close_brace_same_line_empty_type`
- 値: `true`、`false`

**関数の本体が空の場合は、終わりかっこを始めかっこと同じ行に移動する**

- 名前: `cpp_new_line_close_brace_same_line_empty_function`
- 値: `true`、`false`

**新しい行に 'catch' および類似キーワードを配置する**

- 名前: `cpp_new_line_before_catch`
- 値: `true`、`false`

**新しい行に 'else' を配置する**

- 名前: `cpp_new_line_before_else`
- 値: `true`、`false`

**do-while ループの 'while' を新しい行に配置する**

- 名前: `cpp_new_line_before_while_in_do_while`
- 値: `true`、`false`

### <a name="spacing-settings"></a>スペースの設定

**関数名と引数リストの左かっこの間のスペース**

- 名前: `cpp_space_before_function_open_parenthesis`
- 値:
  - `insert` - スペースを挿入する
  - `remove` - スペースを削除する
  - `ignore` - スペースを変更しない

**引数リストのかっこ内にスペースを挿入する**

- 名前 `cpp_space_within_parameter_list_parentheses` 値: `true`、`false`

**引数リストが空の場合に、かっこ間にスペースを挿入する**

- 名前: `cpp_space_between_empty_parameter_list_parentheses`
- 値: `true`、`false`

**制御フロー ステートメント内のキーワードと始めかっこの間にスペースを挿入する**

- 名前: `cpp_space_after_keywords_in_control_flow_statements`
- 値: `true`、`false`

**コントロール ステートメントのかっこ内にスペースを挿入する**

- 名前: `cpp_space_within_control_flow_statement_parentheses`
- 値: `true`、`false`

**ラムダ引数リストの始めかっこの前にスペースを挿入する**

- 名前: `cpp_space_before_lambda_open_parenthesis`
- 値: `true`、`false`

**C スタイル キャストのかっこ内にスペースを挿入する**

- 名前: `cpp_space_within_cast_parentheses`
- 値: `true`、`false`

**C スタイル キャストの終わりかっこの後にスペースを挿入する**

- 名前: `cpp_space_after_cast_close_parenthesis`
- 値: `true`、`false`

**かっこで囲まれた式のかっこ内にスペースを挿入する**

- 名前: `cpp_space_within_expression_parentheses`
- 値: `true`、`false`

**ブロックの左中かっこの前にスペースを挿入する**

- 名前: `cpp_space_before_block_open_brace`
- 値: `true`、`false`

**空のかっこの間にスペースを挿入する**

- 名前: `cpp_space_between_empty_braces`
- 値: `true`、`false`

**均一初期化および初期化子リストの始めかっこの前にスペースを挿入する**

- 名前: `cpp_space_before_initializer_list_open_brace`
- 値: `true`、`false`

**均一初期化および初期化子リストのかっこ内にスペースを挿入する**

- 名前: `cpp_space_within_initializer_list_braces`
- 値: `true`、`false`

**均一初期化および初期化子リストの中にスペースを保持する**

- 名前: `cpp_space_preserve_in_initializer_list`
- 値: `true`、`false`

**始め角かっこの前にスペースを挿入する**

- 名前: `cpp_space_before_open_square_bracket`
- 値: `true`、`false`

**角かっこ内にスペースを挿入する**

- 名前: `cpp_space_within_square_brackets`
- 値: `true`、`false`

**空の角かっこの前にスペースを挿入する**

- 名前: `cpp_space_before_empty_square_brackets`
- 値: `true`、`false`

**空の角かっこの間にスペースを挿入する**

- 名前: `cpp_space_between_empty_square_brackets`
- 値: `true`、`false`

**多次元配列の角かっこをグループ化する**

- 名前: `cpp_space_group_square_brackets`
- 値: `true`、`false`

**ラムダの角かっこ内にスペースを挿入する**

- 名前: `cpp_space_within_lambda_brackets`
- 値: `true`、`false`

**SpaceBetweenEmptyLambdaBrackets**

- 名前: `cpp_space_between_empty_lambda_brackets`
- 値: `true`、`false`

**コンマの前にスペースを挿入する**

- 名前: `cpp_space_before_comma`
- 値: `true`、`false`

**コンマの後にスペースを追加する**

- 名前: `cpp_space_after_comma`
- 値: `true`、`false`

**メンバー演算子の前後のスペースを削除する**

- 名前: `cpp_space_remove_around_member_operators`
- 値: `true`、`false`

**型宣言で、基本のコロンの前にスペースを挿入する**

- 名前: `cpp_space_before_inheritance_colon`
- 値: `true`、`false`

**コンストラクターのコロンの前にスペースを追加する**

- 名前: `cpp_space_before_constructor_colon`
- 値: `true`、`false`

**セミコロンの前のスペースを削除する**

- 名前: `cpp_space_remove_before_semicolon`
- 値: `true`、`false`

**セミコロンの後にスペースを挿入する**

- 名前: `cpp_space_after_semicolon`
- 値: `true`、`false`

**単項演算子とそのオペランドの間のスペースを削除する**

- 名前: `cpp_space_remove_around_unary_operator`
- 値: `true`、`false`

**バイナリ演算子の前後のスペース**

- 名前: `cpp_space_around_binary_operator`
- 値:
  - `insert` - バイナリ演算子の前後にスペースを挿入する。
  - `remove` - バイナリ演算子の前後のスペースを削除する。
  - `ignore` - バイナリ演算子の前後のスペースを変更しない。

**代入演算子の前後のスペース**

- 名前: `cpp_space_around_assignment_operator`
- 値:
  - `insert` - 代入演算子の前後にスペースを挿入する。
  - `remove` - 代入演算子の前後のスペースを削除する。
  - `ignore` - 代入演算子の前後のスペースを変更しない。

**ポインター/参照の配置**

- 名前: `cpp_space_pointer_reference_alignment`
- 値:
  - `left` - 左揃え。
  - `center` - 中央揃え。
  - `right` - 右揃え。
  - `ignore` - 変更しません。

**条件演算子の前後のスペース**

- 名前: `cpp_space_around_ternary_operator`
- 値:
  - `insert` - 条件演算子の前後にスペースを挿入する。
  - `remove` - 条件演算子の前後のスペースを削除する。
  - `ignore` - 条件演算子の前後のスペースを変更しない。

### <a name="wrapping-options"></a>折り返しオプション

**ブロックの折り返しオプション**

- 名前: `cpp_wrap_preserve_blocks`
- 値:
  - `one_liners` - 1 行のコード ブロックを折り返さない。
  - `all_one_line_scopes` - 始めかっこと終わりかっこが次の行にある場合、コード ブロックを折り返さない。
  - `never` - 常にブロックに改行設定を適用する。

## <a name="see-also"></a>関連項目

- [EditorConfig.org](https://editorconfig.org/)
- [言語サービスの EditorConfig のサポート](../extensibility/supporting-editorconfig.md)
- [コード エディターの機能](writing-code-in-the-code-and-text-editor.md)
