---
title: EditorConfig の .NET コーディング規則の設定
ms.date: 02/21/2020
ms.topic: reference
helpviewer_keywords:
- coding conventions [EditorConfig]
- EditorConfig coding conventions
- language code style rules [EditorConfig]
- formatting conventions [EditorConfig]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: e3ca9ed577fd253c81919f49a67c8286fbe28255
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557794"
---
# <a name="net-coding-convention-settings-for-editorconfig"></a>EditorConfig の .NET コーディング規則の設定

[EditorConfig](../ide/create-portable-custom-editor-options.md) ファイルを使用すれば、コードベースで一貫性のあるコード スタイルを定義および維持できます。 EditorConfig には、`indent_style` や `indent_size` などのいくつかの主要な書式設定プロパティが含まれています。 Visual Studio では、EditorConfig ファイルを使用して .NET コーディング規則の設定を構成することもできます。 個々の .NET コーディング規則を有効化または無効化したり、重大度レベルで各規則を適用する程度を構成したりすることができます。

> [!TIP]
> - EditorConfig ファイルでコーディング規則を定義すると、Visual Studio に組み込まれている[コード スタイル アナライザー](../code-quality/roslyn-analyzers-overview.md)でのコード分析の方法が構成されます。 EditorConfig ファイルは、これらのアナライザーに対する構成ファイルです。
> - Visual Studio に対するコードのスタイルのユーザー設定は、[テキスト エディターの [オプション]](code-styles-and-code-cleanup.md) ダイアログで設定することもできます。 ただし、EditorConfig での設定の方が優先され、 **[オプション]** での設定は特定のプロジェクトとは関連付けられません。

## <a name="convention-categories"></a>規則のカテゴリ

サポートされている .NET コーディング規則には次の 3 つのカテゴリがあります。

- [言語規則](../ide/editorconfig-language-conventions.md)

   C# または Visual Basic 言語に関するルール。 たとえば、変数の定義時の `var` または明示的な型の使用や、式形式メンバーの優先に関するルールを指定できます。

- [書式規則](../ide/editorconfig-formatting-conventions.md)

   コードを読みやすくするためのレイアウトや構造に関するルール。 たとえば、Allman 中かっこや、制御ブロックでのスペースの優先に関するルールを指定できます。

- [名前付け規則](../ide/editorconfig-naming-conventions.md)

   コード要素の名前付けに関するルール。 たとえば、`async` メソッドは "Async" で終わる必要があるなどと指定できます。

## <a name="example-editorconfig-file"></a>EditorConfig ファイルの例

作業の開始に役立つように、ここでは既定のオプションを使用する *.editorconfig* ファイルの例を示します。 Visual Studio では、このファイルを生成してプロジェクトに保存するには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]** > **[C#]** または **[Basic]** > **[コード スタイル]**  >  **[全般]** の順に選択します。 次に、 **[設定から editorconfig ファイルを生成]** ボタンをクリックします。 詳細については、「[コードのスタイル設定](code-styles-and-code-cleanup.md)」を参照してください。

```ini
###############################
# Core EditorConfig Options   #
###############################

root = true

# All files
[*]
indent_style = space

# Code files
[*.{cs,csx,vb,vbx}]
indent_size = 4
insert_final_newline = true
charset = utf-8-bom

###############################
# .NET Coding Conventions     #
###############################

[*.{cs,vb}]

# Organize usings
dotnet_sort_system_directives_first = true

# this. preferences
dotnet_style_qualification_for_field = false:silent
dotnet_style_qualification_for_property = false:silent
dotnet_style_qualification_for_method = false:silent
dotnet_style_qualification_for_event = false:silent

# Language keywords vs BCL types preferences
dotnet_style_predefined_type_for_locals_parameters_members = true:silent
dotnet_style_predefined_type_for_member_access = true:silent

# Parentheses preferences
dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_operators = never_if_unnecessary:silent

# Modifier preferences
dotnet_style_require_accessibility_modifiers = for_non_interface_members:silent
dotnet_style_readonly_field = true:suggestion

# Expression-level preferences
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_null_propagation = true:suggestion
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_prefer_is_null_check_over_reference_equality_method = true:silent
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
dotnet_style_prefer_auto_properties = true:silent
dotnet_style_prefer_conditional_expression_over_assignment = true:silent
dotnet_style_prefer_conditional_expression_over_return = true:silent

###############################
# Naming Conventions          #
###############################

# Style Definitions
dotnet_naming_style.pascal_case_style.capitalization             = pascal_case
# Use PascalCase for constant fields  
dotnet_naming_rule.constant_fields_should_be_pascal_case.severity = suggestion
dotnet_naming_rule.constant_fields_should_be_pascal_case.symbols  = constant_fields
dotnet_naming_rule.constant_fields_should_be_pascal_case.style    = pascal_case_style
dotnet_naming_symbols.constant_fields.applicable_kinds            = field
dotnet_naming_symbols.constant_fields.applicable_accessibilities  = *
dotnet_naming_symbols.constant_fields.required_modifiers          = const

###############################
# C# Coding Conventions       #
###############################

[*.cs]

# var preferences
csharp_style_var_for_built_in_types = true:silent
csharp_style_var_when_type_is_apparent = true:silent
csharp_style_var_elsewhere = true:silent

# Expression-bodied members
csharp_style_expression_bodied_methods = false:silent
csharp_style_expression_bodied_constructors = false:silent
csharp_style_expression_bodied_operators = false:silent
csharp_style_expression_bodied_properties = true:silent
csharp_style_expression_bodied_indexers = true:silent
csharp_style_expression_bodied_accessors = true:silent

# Pattern matching preferences
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion

# Null-checking preferences
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = true:suggestion

# Modifier preferences
csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async:suggestion

# Expression-level preferences
csharp_prefer_braces = true:silent
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_prefer_simple_default_expression = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
csharp_style_inlined_variable_declaration = true:suggestion

###############################
# C# Formatting Rules         #
###############################

# New line preferences
csharp_new_line_before_open_brace = all
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_between_query_expression_clauses = true

# Indentation preferences
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = flush_left

# Space preferences
csharp_space_after_cast = false
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_between_method_call_parameter_list_parentheses = false
csharp_space_between_method_declaration_parameter_list_parentheses = false
csharp_space_between_parentheses = false
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_around_binary_operators = before_and_after
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_between_method_call_empty_parameter_list_parentheses = false

# Wrapping preferences
csharp_preserve_single_line_statements = true
csharp_preserve_single_line_blocks = true

###############################
# VB Coding Conventions       #
###############################

[*.vb]

# Modifier preferences
visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async:suggestion
```

## <a name="see-also"></a>関連項目

- [クイック アクション](../ide/quick-actions.md)
- [移植可能なカスタム エディター オプションを作成する](../ide/create-portable-custom-editor-options.md)
- [.NET Compiler Platform "Roslyn" .editorconfig ファイル](https://github.com/dotnet/roslyn/blob/master/.editorconfig)
- [.NET Compiler Platform ランタイム .editorconfig ファイル](https://github.com/dotnet/runtime/blob/master/.editorconfig)
