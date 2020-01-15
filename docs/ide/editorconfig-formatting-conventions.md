---
title: EditorConfig での .NET の書式規則
ms.date: 07/17/2019
ms.topic: reference
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- formatting conventions [EditorConfig]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 64f6a45b3a5cc49cd541ceb905356093ea4ec221
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589228"
---
# <a name="formatting-conventions"></a>書式規則

Visual Studio 用の EditorConfig の書式規則は、次のカテゴリに分類されます。

- [.NET 書式設定](#net-formatting-settings)

- [C# 書式設定](#c-formatting-settings)

## <a name="rule-format"></a>規則形式

書式規則のルールには次の形式があります。

`rule_name = value`

多くのルールでは、`value` に対して `true` (このスタイルを優先する) または `false` (このスタイルを優先しない) を指定します。 他のルールでは、`flush_left` や `before_and_after` のような値を指定して、ルールを適用する状況と場所を記述します。 重要度は指定しません。

## <a name="net-formatting-settings"></a>.NET 書式設定

このセクションの書式ルールは、C# と Visual Basic のコードに適用されます。

- [using の整理](#organize-using-directives)
  - dotnet_sort_system_directives_first
  - dotnet_separate_import_directive_groups

### <a name="organize-using-directives"></a>using ディレクティブの整理

これらの書式ルールは、`using` ディレクティブと `Imports` ステートメントの並べ替えと表示に関係します。

*.editorconfig* ファイルの例:

```ini
# .NET formatting settings
[*.{cs,vb}]
dotnet_sort_system_directives_first = true
dotnet_separate_import_directive_groups = true
```

#### <a name="dotnet_sort_system_directives_first"></a>dotnet\_sort\_system\_directives_first

|||
|-|-|
| **ルール名** | dotnet_sort_system_directives_first |
| **該当言語** | C# および Visual Basic |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - System.* `using` ディレクティブをアルファベット順に並べ替え、他の using ディレクティブの前に配置します。<br /><br />`false` - System.* `using` ディレクティブを他の `using` ディレクティブの前に配置しません。 |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// dotnet_sort_system_directives_first = true
using System.Collections.Generic;
using System.Threading.Tasks;
using Octokit;

// dotnet_sort_system_directives_first = false
using System.Collections.Generic;
using Octokit;
using System.Threading.Tasks;
```

#### <a name="dotnet_separate_import_directive_groups"></a>dotnet\_separate\_import\_directive\_groups

|||
|-|-|
| **ルール名** | dotnet_separate_import_directive_groups |
| **該当言語** | C# および Visual Basic |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.5 |
| **値** | `true` - `using` ディレクティブ グループの間に空白行を配置します。<br /><br />`false` - `using` ディレクティブ グループの間に空白行を配置しません。 |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// dotnet_separate_import_directive_groups = true
using System.Collections.Generic;
using System.Threading.Tasks;

using Octokit;

// dotnet_separate_import_directive_groups = false
using System.Collections.Generic;
using System.Threading.Tasks;
using Octokit;
```

## <a name="c-formatting-settings"></a>C# 書式設定

このセクションの書式ルールは、C# コードにのみ適用されます。

- [改行オプション](#new-line-options)
  - csharp_new_line_before_open_brace
  - csharp_new_line_before_else
  - csharp_new_line_before_catch
  - csharp_new_line_before_finally
  - csharp_new_line_before_members_in_object_initializers
  - csharp_new_line_before_members_in_anonymous_types
  - csharp_new_line_between_query_expression_clauses
- [インデント オプション](#indentation-options)
  - csharp_indent_case_contents
  - csharp_indent_switch_labels
  - csharp_indent_labels
  - csharp_indent_block_contents
  - csharp_indent_braces
  - csharp_indent_case_contents_when_block
- [スペース オプション](#spacing-options)
  - csharp_space_after_cast
  - csharp_space_after_keywords_in_control_flow_statements
  - csharp_space_between_parentheses
  - csharp_space_before_colon_in_inheritance_clause
  - csharp_space_after_colon_in_inheritance_clause
  - csharp_space_around_binary_operators
  - csharp_space_between_method_declaration_parameter_list_parentheses
  - csharp_space_between_method_declaration_empty_parameter_list_parentheses
  - csharp_space_between_method_declaration_name_and_open_parenthesis
  - csharp_space_between_method_call_parameter_list_parentheses
  - csharp_space_between_method_call_empty_parameter_list_parentheses
  - csharp_space_between_method_call_name_and_opening_parenthesis
  - csharp_space_after_comma
  - csharp_space_before_comma
  - csharp_space_after_dot
  - csharp_space_before_dot
  - csharp_space_after_semicolon_in_for_statement
  - csharp_space_before_semicolon_in_for_statement
  - csharp_space_around_declaration_statements
  - csharp_space_before_open_square_brackets
  - csharp_space_between_empty_square_brackets
  - csharp_space_between_square_brackets
- [折り返しオプション](#wrap-options)
  - csharp_preserve_single_line_statements
  - csharp_preserve_single_line_blocks

### <a name="new-line-options"></a>改行オプション

これらの書式ルールは、コードの書式を設定する場合の改行の使用に関するものです。

*.editorconfig* ファイルの例:

```ini
# CSharp formatting settings:
[*.cs]
csharp_new_line_before_open_brace = methods, properties, control_blocks, types
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_between_query_expression_clauses = true
```

#### <a name="csharp_new_line_before_open_brace"></a>csharp\_new\_line\_before\_open_brace

このルールは、左中かっこ (`{`) を前のコードと同じ行に配置するか、新しい行に配置するかに関するものです。 このルールでは、**all**、**none**、または **methods** や **properties** などの 1 つ以上のコード要素を指定して、このルールを適用する必要があるタイミングを定義します。 複数のコード要素を指定するには、コンマ (,) で区切ります。

|||
|-|-|
| **ルール名** | csharp_new_line_before_open_brace |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `all` - 中かっこはすべての式の新しい行に配置する必要があります ("Allman" スタイル)。<br /><br />`none` - 中かっこはすべての式の同じ行に配置する必要があります ("K&R")。<br /><br />`accessors`、`anonymous_methods`、`anonymous_types`、`control_blocks`、`events`、`indexers`、`lambdas`、`local_functions`、`methods`、`object_collection_array_initializers`、`properties`、`types` - 中かっこは指定されたコード要素の新しい行に配置する必要があります ("Allman" スタイル)。 |
| **Visual Studio の既定値** | `all` |

コード例:

```csharp
// csharp_new_line_before_open_brace = all
void MyMethod()
{
    if (...)
    {
        ...
    }
}

// csharp_new_line_before_open_brace = none
void MyMethod() {
    if (...) {
        ...
    }
}
```

#### <a name="csharp_new_line_before_else"></a>csharp\_new\_line\_before_else

|||
|-|-|
| **ルール名** | csharp_new_line_before_else |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - 新しい行に `else` ステートメントを配置します。<br /><br />`false` - 同じ行に `else` ステートメントを配置します。 |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_new_line_before_else = true
if (...) {
    ...
}
else {
    ...
}

// csharp_new_line_before_else = false
if (...) {
    ...
} else {
    ...
}
```

#### <a name="csharp_new_line_before_catch"></a>csharp\_new\_line\_before_catch

|||
|-|-|
| **ルール名** | csharp_new_line_before_catch |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - 新しい行に `catch` ステートメントを配置します。<br /><br />`false` - 同じ行に `catch` ステートメントを配置します。 |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_new_line_before_catch = true
try {
    ...
}
catch (Exception e) {
    ...
}

// csharp_new_line_before_catch = false
try {
    ...
} catch (Exception e) {
    ...
}
```

#### <a name="csharp_new_line_before_finally"></a>csharp\_new\_line\_before_finally

|||
|-|-|
| **ルール名** | csharp_new_line_before_finally |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - `finally` ステートメントを右中かっこの後の新しい行に配置する必要があります。<br /><br />`false` - `finally` ステートメントを右中かっこと同じ行に配置する必要があります。 |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_new_line_before_finally = true
try {
    ...
}
catch (Exception e) {
    ...
}
finally {
    ...
}

// csharp_new_line_before_finally = false
try {
    ...
} catch (Exception e) {
    ...
} finally {
    ...
}
```

#### <a name="csharp_new_line_before_members_in_object_initializers"></a>csharp\_new\_line\_before\_members\_in\_object_initializers

|||
|-|-|
| **ルール名** | csharp_new_line_before_members_in_object_initializers |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - オブジェクト初期化子のメンバーを別の行に配置する必要があります<br /><br />`false` - オブジェクト初期化子のメンバーを同じ行に配置する必要があります |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_new_line_before_members_in_object_initializers = true
var z = new B()
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_object_initializers = false
var z = new B()
{
    A = 3, B = 4
}
```

#### <a name="csharp_new_line_before_members_in_anonymous_types"></a>csharp\_new\_line\_before\_members\_in\_anonymous_types

|||
|-|-|
| **ルール名** | csharp_new_line_before_members_in_anonymous_types |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - 匿名型のメンバーを別の行に配置する必要があります<br /><br />`false` - 匿名型のメンバーを同じ行に配置する必要があります |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_new_line_before_members_in_anonymous_types = true
var z = new
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_anonymous_types = false
var z = new
{
    A = 3, B = 4
}
```

#### <a name="csharp_new_line_between_query_expression_clauses"></a>csharp_new_line_between_query_expression_clauses

|||
|-|-|
| **ルール名** | csharp_new_line_between_query_expression_clauses |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - クエリ式の句の要素を別の行に配置する必要があります<br /><br />`false` - クエリ式の句の要素を同じ行に配置する必要があります |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_new_line_between_query_expression_clauses = true
var q = from a in e
        from b in e
        select a * b;

// csharp_new_line_between_query_expression_clauses = false
var q = from a in e from b in e
        select a * b;
```

### <a name="indentation-options"></a>インデント オプション

これらの書式ルールは、コードの書式を設定する場合のインデントの使用に関するものです。

*.editorconfig* ファイルの例:

```ini
# CSharp formatting settings:
[*.cs]
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = flush_left
csharp_indent_block_contents = true
csharp_indent_braces = false
csharp_indent_case_contents_when_block = true
```

#### <a name="csharp_indent_case_contents"></a>csharp\_indent\_case_contents

|||
|-|-|
| **ルール名** | csharp_indent_case_contents |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - `switch` ケース コンテンツにインデントを付けます<br /><br />`false` - `switch` ケース コンテンツにインデントを付けません |
| **Visual Studio の既定値** | `true` |

- このルールが **true** に設定されている場合は、i。
- このルールが **false** に設定されている場合は、d。

コード例:

```csharp
// csharp_indent_case_contents = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_case_contents = false
switch(c) {
    case Color.Red:
    Console.WriteLine("The color is red");
    break;
    case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
    default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

#### <a name="csharp_indent_switch_labels"></a>csharp\_indent\_switch_labels

|||
|-|-|
| **ルール名** | csharp_indent_switch_labels |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - `switch` ラベルをインデントします<br /><br />`false` - `switch` ラベルをインデントしません |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_indent_switch_labels = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_switch_labels = false
switch(c) {
case Color.Red:
    Console.WriteLine("The color is red");
    break;
case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

#### <a name="csharp_indent_labels"></a>csharp\_indent_labels

|||
|-|-|
| **ルール名** | csharp_indent_labels |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `flush_left` - ラベルは左端の列に配置されます<br /><br />`one_less_than_current` - ラベルは、現在のコンテキストのインデントを 1 つ減らした位置に配置されます<br /><br />`no_change` - ラベルは、現在のコンテキストと同じインデントで配置されます |
| **Visual Studio の既定値** | `no_change` |

コード例:

```csharp
// csharp_indent_labels= flush_left
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
error:
        throw new Exception(...);
    }
}

// csharp_indent_labels = one_less_than_current
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
    error:
        throw new Exception(...);
    }
}

// csharp_indent_labels= no_change
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
        error:
        throw new Exception(...);
    }
}
```

#### <a name="csharp_indent_block_contents"></a>csharp_indent_block_contents

|||
|-|-|
| **ルール名** | csharp_indent_block_contents |
| **該当言語** | C# |
| **値** | `true` - <br /><br />`false` -  |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_indent_block_contents = true
static void Hello()
{
    Console.WriteLine("Hello");
}

// csharp_indent_block_contents = false
static void Hello()
{
Console.WriteLine("Hello");
}
```

#### <a name="csharp_indent_braces"></a>csharp_indent_braces

|||
|-|-|
| **ルール名** | csharp_indent_braces |
| **該当言語** | C# |
| **値** | `true` - <br /><br />`false` -  |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_indent_braces = true
static void Hello()
    {
    Console.WriteLine("Hello");
    }

// csharp_indent_braces = false
static void Hello()
{
    Console.WriteLine("Hello");
}
```

#### <a name="csharp_indent_case_contents_when_block"></a>csharp_indent_case_contents_when_block

|||
|-|-|
| **ルール名** | csharp_indent_case_contents_when_block |
| **該当言語** | C# |
| **値** | `true` - <br /><br />`false` -  |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_indent_case_contents_when_block = true
case 0:
    {
        Console.WriteLine("Hello");
        break;
    }

// csharp_indent_case_contents_when_block = false
case 0:
{
    Console.WriteLine("Hello");
    break;
}
```

### <a name="spacing-options"></a>スペース オプション

これらの書式ルールは、コードの書式を設定する場合の空白文字の使用に関するものです。

*.editorconfig* ファイルの例:

```ini
# CSharp formatting settings:
[*.cs]
csharp_space_after_cast = true
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_between_parentheses = control_flow_statements, type_casts
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_around_binary_operators = before_and_after
csharp_space_between_method_declaration_parameter_list_parentheses = true
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_declaration_name_and_open_parenthesis = false
csharp_space_between_method_call_parameter_list_parentheses = true
csharp_space_between_method_call_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_after_comma = true
csharp_space_before_comma = false
csharp_space_after_dot = false
csharp_space_before_dot = false
csharp_space_after_semicolon_in_for_statement = true
csharp_space_before_semicolon_in_for_statement = false
csharp_space_around_declaration_statements = false
csharp_space_before_open_square_brackets = false
csharp_space_between_empty_square_brackets = false
csharp_space_between_square_brackets = false
```

#### <a name="csharp_space_after_cast"></a>csharp\_space\_after_cast

|||
|-|-|
| **ルール名** | csharp_space_after_cast |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - キャストと値の間に空白文字を配置します<br /><br />`false` - キャストと値の間の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_after_cast = true
int y = (int) x;

// csharp_space_after_cast = false
int y = (int)x;
```

#### <a name="csharp_space_after_keywords_in_control_flow_statements"></a>csharp_space_after_keywords_in_control_flow_statements

|||
|-|-|
| **ルール名** | csharp_space_after_keywords_in_control_flow_statements |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - `for` ループなど、制御フロー ステートメントのキーワードの後に空白文字を配置します<br /><br />`false` - `for` ループなど、制御フロー ステートメントのキーワードの後の空白文字を削除します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_space_after_keywords_in_control_flow_statements = true
for (int i;i<x;i++) { ... }

// csharp_space_after_keywords_in_control_flow_statements = false
for(int i;i<x;i++) { ... }
```

#### <a name="csharp_space_between_parentheses"></a>csharp_space_between_parentheses

|||
|-|-|
| **ルール名** | csharp_space_between_parentheses |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `control_flow_statements` - 制御フロー ステートメントのかっこの間にスペースを配置します<br /><br />`expressions` - 式のかっこの間にスペースを配置します<br /><br />`type_casts` - 型キャストのかっこの間にスペースを配置します |
| **Visual Studio の既定値** | `false` |

このルールを省略するか、`control_flow_statements`、`expressions`、または `type_casts` 以外の値を使用する場合、設定は適用されません。

コード例:

```csharp
// csharp_space_between_parentheses = control_flow_statements
for ( int i = 0; i < 10; i++ ) { }

// csharp_space_between_parentheses = expressions
var z = ( x * y ) - ( ( y - x ) * 3 );

// csharp_space_between_parentheses = type_casts
int y = ( int )x;
```

#### <a name="csharp_space_before_colon_in_inheritance_clause"></a>csharp\_space\_before\_colon\_in\_inheritance_clause

|||
|-|-|
| **ルール名** | csharp_space_before_colon_in_inheritance_clause |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.7 |
| **値** | `true` - 型宣言ではベースまたはインターフェイスのコロンの前に空白文字を配置します<br /><br />`false` - 型宣言ではベースまたはインターフェイスのコロンの前の空白文字を除去します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_space_before_colon_in_inheritance_clause = true
interface I
{

}

class C : I
{

}

// csharp_space_before_colon_in_inheritance_clause = false
interface I
{

}

class C: I
{

}
```

#### <a name="csharp_space_after_colon_in_inheritance_clause"></a>csharp\_space\_after\_colon\_in\_inheritance_clause

|||
|-|-|
| **ルール名** | csharp_space_after_colon_in_inheritance_clause |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.7 |
| **値** | `true` - 型宣言ではベースまたはインターフェイスのコロンの後に空白文字を配置します<br /><br />`false` - 型宣言ではベースまたはインターフェイスのコロンの後の空白文字を削除します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_space_after_colon_in_inheritance_clause = true
interface I
{

}

class C : I
{

}

// csharp_space_after_colon_in_inheritance_clause = false
interface I
{

}

class C :I
{

}
```

#### <a name="csharp_space_around_binary_operators"></a>csharp\_space\_around\_binary_operators

|||
|-|-|
| **ルール名** | csharp_space_around_binary_operators |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.7 |
| **値** | `before_and_after` - バイナリ演算子の前後にスペースを挿入します<br /><br />`none` - バイナリ演算子の前後のスペースを削除します<br /><br />`ignore` - バイナリ演算子の前後のスペースを無視します |
| **Visual Studio の既定値** | `before_and_after` |

このルールを省略するか、`before_and_after`、`none`、または `ignore` 以外の値を使用する場合、設定は適用されません。

コード例:

```csharp
// csharp_space_around_binary_operators = before_and_after
return x * (x - y);

// csharp_space_around_binary_operators = none
return x*(x-y);

// csharp_space_around_binary_operators = ignore
return x  *  (x-y);
```

#### <a name="csharp_space_between_method_declaration_parameter_list_parentheses"></a>csharp_space_between_method_declaration_parameter_list_parentheses

|||
|-|-|
| **ルール名** | csharp_space_between_method_declaration_parameter_list_parentheses |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - メソッド宣言パラメーター リストの始めかっこの後と終わりかっこの前に空白文字を配置します<br /><br />`false` - メソッド宣言パラメーター リストの始めかっこの後と終わりかっこの前の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_method_declaration_parameter_list_parentheses = true
void Bark( int x ) { ... }

// csharp_space_between_method_declaration_parameter_list_parentheses = false
void Bark(int x) { ... }
```

#### <a name="csharp_space_between_method_declaration_empty_parameter_list_parentheses"></a>csharp_space_between_method_declaration_empty_parameter_list_parentheses

|||
|-|-|
| **ルール名** | csharp_space_between_method_declaration_empty_parameter_list_parentheses |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.7 |
| **値** | `true` - メソッド宣言の空のパラメーター リストのかっこ内にスペースを挿入します<br /><br />`false` - メソッド宣言の空のパラメーター リストのかっこ内にスペースを削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_method_declaration_empty_parameter_list_parentheses = true
void Goo( )
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}

// csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

#### <a name="csharp_space_between_method_declaration_name_and_open_parenthesis"></a>csharp_space_between_method_declaration_name_and_open_parenthesis

|||
|-|-|
| **ルール名** | csharp_space_between_method_declaration_name_and_open_parenthesis |
| **該当言語** | C# |
| **値** | `true` - メソッド宣言のメソッド名と始めかっこの間に空白文字を配置します<br /><br />`false` - メソッド宣言のメソッド名と始めかっこの間の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_method_declaration_name_and_open_parenthesis = true
void M () { }

// csharp_space_between_method_declaration_name_and_open_parenthesis = false
void M() { }
```

#### <a name="csharp_space_between_method_call_parameter_list_parentheses"></a>csharp_space_between_method_call_parameter_list_parentheses

|||
|-|-|
| **ルール名** | csharp_space_between_method_call_parameter_list_parentheses |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - メソッド呼び出しの始めかっこの後と終わりかっこの前に空白文字を配置します<br /><br />`false` - メソッド呼び出しの始めかっこの後と終わりかっこの前の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_method_call_parameter_list_parentheses = true
MyMethod( argument );

// csharp_space_between_method_call_parameter_list_parentheses = false
MyMethod(argument);
```

#### <a name="csharp_space_between_method_call_empty_parameter_list_parentheses"></a>csharp_space_between_method_call_empty_parameter_list_parentheses

|||
|-|-|
| **ルール名** | csharp_space_between_method_call_empty_parameter_list_parentheses |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.7 |
| **値** | `true` - 空の引数リストのかっこ内にスペースを挿入します<br /><br />`false` - 空の引数リストのかっこ内にスペースを削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_method_call_empty_parameter_list_parentheses = true
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo( );
}

// csharp_space_between_method_call_empty_parameter_list_parentheses = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

#### <a name="csharp_space_between_method_call_name_and_opening_parenthesis"></a>csharp_space_between_method_call_name_and_opening_parenthesis

|||
|-|-|
| **ルール名** | csharp_space_between_method_call_name_and_opening_parenthesis |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.7 |
| **値** | `true` - メソッド呼び出し名と左かっこの間にスペースを挿入します<br /><br />`false` - メソッド呼び出し名と左かっこの間にスペースを削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_method_call_name_and_opening_parenthesis = true
void Goo()
{
    Goo (1);
}

void Goo(int x)
{
    Goo ();
}

// csharp_space_between_method_call_name_and_opening_parenthesis = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

#### <a name="csharp_space_after_comma"></a>csharp_space_after_comma

|||
|-|-|
| **ルール名** | csharp_space_after_comma |
| **該当言語** | C# |
| **値** | `true` - コンマの後にスペースを挿入します<br /><br />`false` - コンマの後のスペースを削除します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_space_after_comma = true
int[] x = new int[] { 1, 2, 3, 4, 5 };

// csharp_space_after_comma = false
int[] x = new int[] { 1,2,3,4,5 }
```

#### <a name="csharp_space_before_comma"></a>csharp_space_before_comma

|||
|-|-|
| **ルール名** | csharp_space_before_comma |
| **該当言語** | C# |
| **値** | `true` - コンマの前に空白文字を挿入します<br /><br />`false` - コンマの前の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_before_comma = true
int[] x = new int[] { 1 , 2 , 3 , 4 , 5 };

// csharp_space_before_comma = false
int[] x = new int[] { 1, 2, 3, 4, 5 };
```

#### <a name="csharp_space_after_dot"></a>csharp_space_after_dot

|||
|-|-|
| **ルール名** | csharp_space_after_dot |
| **該当言語** | C# |
| **値** | `true` - ドットの後にスペースを挿入します<br /><br />`false` - ドットの後のスペースを削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_after_dot = true
this. Goo();

// csharp_space_after_dot = false
this.Goo();
```

#### <a name="csharp_space_before_dot"></a>csharp_space_before_dot

|||
|-|-|
| **ルール名** | csharp_space_before_dot |
| **該当言語** | C# |
| **値** | `true` - ドットの前に空白文字を挿入します <br /><br />`false` - ドットの前の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_before_dot = true
this .Goo();

// csharp_space_before_dot = false
this.Goo();
```

#### <a name="csharp_space_after_semicolon_in_for_statement"></a>csharp_space_after_semicolon_in_for_statement

|||
|-|-|
| **ルール名** | csharp_space_after_semicolon_in_for_statement |
| **該当言語** | C# |
| **値** | `true` - `for` ステートメントの各セミコロンの後に空白文字を挿入します<br /><br />`false` - `for` ステートメントの各セミコロンの後の空白文字を削除します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
// csharp_space_after_semicolon_in_for_statement = true
for (int i = 0; i < x.Length; i++)

// csharp_space_after_semicolon_in_for_statement = false
for (int i = 0;i < x.Length;i++)
```

##### <a name="csharp_space_before_semicolon_in_for_statement"></a>csharp_space_before_semicolon_in_for_statement

|||
|-|-|
| **ルール名** | csharp_space_before_semicolon_in_for_statement |
| **該当言語** | C# |
| **値** | `true` - `for` ステートメントの各セミコロンの前に空白文字を挿入します <br /><br />`false` - `for` ステートメントの各セミコロンの前の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_before_semicolon_in_for_statement = true
for (int i = 0 ; i < x.Length ; i++)

// csharp_space_before_semicolon_in_for_statement = false
for (int i = 0; i < x.Length; i++)
```

#### <a name="csharp_space_around_declaration_statements"></a>csharp_space_around_declaration_statements

|||
|-|-|
| **ルール名** | csharp_space_around_declaration_statements |
| **該当言語** | C# |
| **値** | `ignore` - 宣言ステートメント内の余分な空白文字を削除しません<br /><br />`false` - 宣言ステートメント内の余分な空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_around_declaration_statements = ignore
int    x    =    0   ;

// csharp_space_around_declaration_statements = false
int x = 0;
```

#### <a name="csharp_space_before_open_square_brackets"></a>csharp_space_before_open_square_brackets

|||
|-|-|
| **ルール名** | csharp_space_before_open_square_brackets |
| **該当言語** | C# |
| **値** | `true` - 始め角かっこ `[` の前に空白文字を挿入します <br /><br />`false` - 始め角かっこ `[` の前の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_before_open_square_brackets = true
int [] numbers = new int [] { 1, 2, 3, 4, 5 };

// csharp_space_before_open_square_brackets = false
int[] numbers = new int[] { 1, 2, 3, 4, 5 };
```

#### <a name="csharp_space_between_empty_square_brackets"></a>csharp_space_between_empty_square_brackets

|||
|-|-|
| **ルール名** | csharp_space_between_empty_square_brackets |
| **該当言語** | C# |
| **値** | `true` - 空の角かっこ `[ ]` の間に空白文字を挿入します <br /><br />`false` - 空の角かっこ `[]` の間の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_empty_square_brackets = true
int[ ] numbers = new int[ ] { 1, 2, 3, 4, 5 };

// csharp_space_between_empty_square_brackets = false
int[] numbers = new int[] { 1, 2, 3, 4, 5 };
```

#### <a name="csharp_space_between_square_brackets"></a>csharp_space_between_square_brackets

|||
|-|-|
| **ルール名** | csharp_space_between_square_brackets |
| **該当言語** | C# |
| **値** | `true` - 空ではない角かっこ `[ 0 ]` に空白文字を挿入します <br /><br />`false` - 空ではない角かっこ `[0]` の空白文字を削除します |
| **Visual Studio の既定値** | `false` |

コード例:

```csharp
// csharp_space_between_square_brackets = true
int index = numbers[ 0 ];

// csharp_space_between_square_brackets = false
int index = numbers[0];
```

### <a name="wrap-options"></a>折り返しオプション

これらの書式ルールは、ステートメントとコード ブロックでの 1 行と別の行の使用に関するものです。

*.editorconfig* ファイルの例:

```ini
# CSharp formatting settings:
[*.cs]
csharp_preserve_single_line_statements = true
csharp_preserve_single_line_blocks = true
```

#### <a name="csharp_preserve_single_line_statements"></a>csharp_preserve_single_line_statements

|||
|-|-|
| **ルール名** | csharp_preserve_single_line_statements |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - 1 行に複数のステートメントとメンバー宣言を表示します<br /><br />`false` - 別の行にステートメントとメンバー宣言を表示します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
//csharp_preserve_single_line_statements = true
int i = 0; string name = "John";

//csharp_preserve_single_line_statements = false
int i = 0;
string name = "John";
```

#### <a name="csharp_preserve_single_line_blocks"></a>csharp_preserve_single_line_blocks

|||
|-|-|
| **ルール名** | csharp_preserve_single_line_blocks |
| **該当言語** | C# |
| **導入されたバージョン** | Visual Studio 2017 バージョン 15.3 |
| **値** | `true` - コード ブロックを単一行に配置します<br /><br />`false` - コード ブロックを別の行に配置します |
| **Visual Studio の既定値** | `true` |

コード例:

```csharp
//csharp_preserve_single_line_blocks = true
public int Foo { get; set; }

//csharp_preserve_single_line_blocks = false
public int MyProperty
{
    get; set;
}
```

## <a name="see-also"></a>関連項目

- [言語規則](editorconfig-language-conventions.md)
- [名前付け規則](editorconfig-naming-conventions.md)
- [EditorConfig の .NET コーディング規則の設定](editorconfig-code-style-settings-reference.md)
