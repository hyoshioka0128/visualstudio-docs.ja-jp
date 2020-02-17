---
title: 規則セットを使用した実行対象の C++ 規則の指定
ms.date: 04/28/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.native
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: ec2d9c812de9ec6be5ba5f42ca2a4484703d0b84
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271785"
---
# <a name="use-rule-sets-to-specify-the-c-rules-to-run"></a>規則セットを使用してC++実行する規則を指定する

Visual Studio では、コード分析に関連する特定のプロジェクトのニーズに合わせてカスタム*規則セット*を作成および変更できます。 既定の規則セットは `%VSINSTALLDIR%\Team Tools\Static Analysis Tools\Rule Sets`に格納されます。

**Visual Studio 2017 バージョン15.7 以降:** 任意のテキストエディターを使用してカスタム規則セットを作成し、使用しているビルドシステムに関係なく、コマンドラインビルドで適用できます。 詳細については、「 [/analyze: ルールセット](/cpp/build/reference/analyze-code-analysis)」を参照してください。

Visual Studio でカスタムC++規則セットを作成するには、VISUALC++ studio IDE で C/プロジェクトを開く必要があります。 次に、規則セットエディターで標準規則セットを開き、特定の規則を追加または削除し、必要に応じて、コード分析によって規則に違反したと判断されたときに発生するアクションを変更します。

新規のカスタム規則セットを作成する場合は、新しいファイル名を使用して保存します。 作成したカスタム規則セットは、自動的にプロジェクトに割り当てられます。

## <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>既存の 1 つの規則セットからカスタム規則を作成するには

1. ソリューションエクスプローラーで、プロジェクトのショートカットメニューを開き、 **[プロパティ]** を選択します。

2. **[プロパティ]** タブで、 **[コード分析]** を選択します。

3. **[規則セット]** ドロップダウンリストで、次のいずれかの操作を行います。

   - カスタマイズする規則セットを選択します。

     \- - または -

   - 参照\<を選択してください.. **.** 一覧に含まれていない既存の規則セットを指定する場合は > します。

4. **[開く]** を選択すると、ルールセットエディターにルールが表示されます。

## <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>規則セット エディターで規則セットを変更するには

- ルールセットの表示名を変更するには、 **[表示]** メニューの **[プロパティウィンドウ]** をクリックします。 **[名前]** ボックスに表示名を入力します。 表示名には、ファイル名と異なる名前を指定できます。

- グループ内のすべての規則をカスタム規則セットに追加するには、グループのチェック ボックスをオンにします。 グループ内のすべての規則を削除するには、チェック ボックスをオフにします。

- 特定の規則をカスタム規則セットに追加するには、その規則のチェック ボックスをオンにします。 規則セットから規則を削除するには、チェック ボックスをオフにします。

- コード分析でルールに違反したときに実行されるアクションを変更するには、ルールの **[アクション]** フィールドを選択して、次のいずれかの値を選択します。

     **警告**-警告を生成します。

     **エラー** -エラーが生成されます。
     
     **Info** -メッセージを生成します。

     **None** -ルールを無効にします。 このアクションは、規則セットから規則を削除するのと同じです。

## <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>規則セット エディターのツール バーを使用して、規則セット エディターに表示されるフィールドのグループ化、フィルター処理、または変更を行うには

- すべてのグループのルールを展開するには、 **[すべて展開]** を選択します。

- すべてのグループのルールを折りたたむには、 **[すべて折りたたみ]** を選択します。

- ルールがグループ化されているフィールドを変更するには、 **[グループ化]** ボックスの一覧からフィールドを選択します。 グループ化されていない規則を表示するには **\<[なし] >** を選択します。

- ルール列のフィールドを追加または削除するには、 **[列のオプション]** を選択します。

- 現在のソリューションに適用されない規則を非表示にするには、[**現在のソリューションに適用されない規則を非表示**にする] を選択します。

- エラーアクションが割り当てられているルールの表示と非表示を切り替えるには、[**コード分析エラーを生成するルールを表示**する] を選択します。

- 警告アクションが割り当てられている規則の表示と非表示を切り替えるには、[**コード分析警告を生成できる規則を表示**する] を選択します。

- **[なし**] アクションが割り当てられているルールの表示と非表示を切り替えるには、[無効になっている**ルールを表示**する] を選択します。

- 現在の規則セットに Microsoft の既定の規則セットを追加または削除するには、 **[子規則セットの追加または削除]** を選択します。

## <a name="to-create-a-rule-set-in-a-text-editor"></a>テキストエディターでルールセットを作成するには

カスタム規則セットは、テキストエディターで作成し、`.ruleset` 拡張機能を持つ任意の場所に格納し、 [/analyze: ルールセット](/cpp/build/reference/analyze-code-analysis)コンパイラオプションを使用してで適用できます。

次の例は、開始点として使用できる基本的な規則セットファイルを示しています。

::: moniker range="vs-2017"

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="New Rule Set" Description=" " ToolsVersion="15.0">
  <Rules AnalyzerId="Microsoft.Analyzers.NativeCodeAnalysis" RuleNamespace="Microsoft.Rules.Native">
    <Rule Id="C6001" Action="Warning" />
    <Rule Id="C26494" Action="Warning" />
  </Rules>
</RuleSet>
```

::: moniker-end

::: moniker range=">=vs-2019"

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="New Rule Set" Description=" " ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.NativeCodeAnalysis" RuleNamespace="Microsoft.Rules.Native">
    <Rule Id="C6001" Action="Warning" />
    <Rule Id="C26494" Action="Warning" />
  </Rules>
</RuleSet>
```

::: moniker-end
