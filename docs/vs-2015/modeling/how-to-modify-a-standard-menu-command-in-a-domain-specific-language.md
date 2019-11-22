---
title: 'How to: Modify a Standard Menu Command in a Domain-Specific Language | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- .vsct files, adding commands to a domain-specific language
- Domain-Specific Language, adding custom commands
ms.assetid: 9b9d8314-d0d8-421a-acb9-d7e91e69825c
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 989367d395abb56e4f57c4aa2694b5f4ef17fb6e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300869"
---
# <a name="how-to-modify-a-standard-menu-command-in-a-domain-specific-language"></a>方法: ドメイン固有言語における標準のメニュー コマンドを修正する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL で自動的に定義される標準コマンドのいくつかの動作を変更できます。 For example, you could modify **Cut** so that it excludes sensitive information. そのためには、コマンド セット クラス内でメソッドをオーバーライドします。 これらのクラスは DslPackage プロジェクト内の CommandSet.cs ファイルで定義され、<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> から派生します。

 要約すると、コマンドを変更するには以下の操作を実行します。

1. [Discover what commands you can modify](#what).

2. [Create a partial declaration of the appropriate command set class](#extend).

3. [Override the ProcessOnStatus and ProcessOnMenu methods](#override) for the command.

   このトピックではこの手順を説明します。

> [!NOTE]
> If you want to create your own menu commands, see [How to: Add a Command to the Shortcut Menu](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

## <a name="what"></a> What commands can you modify?

#### <a name="to-discover-what-commands-you-can-modify"></a>変更可能なコマンドを見つけるには

1. In the `DslPackage` project, open `GeneratedCode\CommandSet.cs`. This C# file can be found in Solution Explorer as a subsidiary of `CommandSet.tt`.

2. Find classes in this file whose names end with "`CommandSet`", for example `Language1CommandSet` and `Language1ClipboardCommandSet`.

3. 各コマンド セット クラスで、"`override`" とその後に続けて空白文字を 1 つ入力します。 IntelliSense ではオーバーライド可能なメソッドの一覧が表示されます。 各コマンドには名前が "`ProcessOnStatus`" および "`ProcessOnMenu`" で始まるメソッドのペアが含まれます。

4. 変更するコマンドを含むコマンド セット クラスをメモします。

5. 編集内容を保存せずにファイルを閉じます。

    > [!NOTE]
    > 通常、生成されたファイルを編集できません。 次回ファイルが生成されたときに編集内容は失われます。

## <a name="extend"></a> Extend the appropriate command set class
 コマンド セット クラスの部分宣言を含む新しいファイルを作成します。

#### <a name="to-extend-the-command-set-class"></a>コマンド セット クラスを拡張するには

1. ソリューション エクスプローラーで、DslPackage プロジェクト内の GeneratedCode フォルダーを開き、CommandSet.tt の下で、生成されたファイル CommandSet.cs を開きます。 名前空間と、名前空間で定義されている最初のクラスの名前を書きとめます。 たとえば、次のように表示されることがあります。

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. In **DslPackage**, create a folder named **Custom Code**. In this folder, create a new class file named `CommandSet.cs`.

3. 新しいファイル内に、生成された部分クラスと同じ名前空間および名前を持つ部分宣言を記述します。 (例:

    ```
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Design;
    namespace Company.Language1 /* Make sure this is correct */
    { internal partial class Language1CommandSet { ...
    ```

     **Note** If you used the class file template to create the new file, you must correct both the namespace and the class name.

## <a name="override"></a> Override the command methods
 Most commands have two associated methods: The method with a name like `ProcessOnStatus`... determines whether the command should be visible and enabled. このメソッドはユーザーが図を右クリックするたびに呼び出され、すばやく実行し、何の変更も生じません。 `ProcessOnMenu`... is called when the user clicks the command, and should perform the function of the command. これらのメソッドの一方または両方をオーバーライドする場合があります。

### <a name="to-change-when-the-command-appears-on-a-menu"></a>メニュー上にコマンドが表示されるタイミングを変更するには
 Override the ProcessOnStatus... method. このメソッドは、パラメーター MenuCommand の Visible プロパティおよび Enabled プロパティを設定します。 通常、コマンドは this.CurrentSelection を見て、コマンドが選択された要素に適用されるかどうかを判断し、それらのプロパティを見て、コマンドが現在の状態で適用可能かどうかを判断します。

 一般的なガイドとして、Visible プロパティは選択される要素により判断する必要があります。 Enabled プロパティは、コマンドがメニュー上に黒で表示されるかグレーで表示されるかを決め、現在の選択状態に依存します。

 以下の例では、ユーザーが複数の図形を選択している場合、[削除] メニュー項目が無効になります。

> [!NOTE]
> このメソッドはコマンドがキーストロークにより使用可能かどうかに影響しません。 たとえば、[削除] メニュー項目を無効化しても、コマンドが Delete キーから呼び出されるのを妨げません。

```
/// <summary>
/// Called when user right-clicks on the diagram or clicks the Edit menu.
/// </summary>
/// <param name="command">Set Visible and Enabled properties.</param>
protected override void ProcessOnStatusDeleteCommand (MenuCommand command)
{
  // Default settings from the base method.
  base.ProcessOnStatusDeleteCommand(command);
  if (this.CurrentSelection.Count > 1)
  {
    // If user has selected more than one item, Delete is greyed out.
    command.Enabled = false;
  }
}
```

 最初に基本的なメソッドを呼び出し、関係のないケースおよび設定のすべてに対処することを推奨します。

 ProcessOnStatus メソッドは、ストア内の要素の作成、削除、または更新を実行しません。

### <a name="to-change-the-behavior-of-the-command"></a>コマンドの動作を変更するには
 Override the ProcessOnMenu... method. 以下の例では、Delete キーを使用しても、ユーザーは一度に複数の要素を削除できません。

```
/// <summary>
/// Called when user presses Delete key
/// or clicks the Delete command on a menu.
/// </summary>
protected override void ProcessOnMenuDeleteCommand()
{
  // Allow users to delete only one thing at a time.
  if (this.CurrentSelection.Count <= 1)
  {
    base.ProcessOnMenuDeleteCommand();
  }
}
```

 要素またはリンクの作成、削除、または更新など、コードがストアに対して変更を加える場合、トランザクション内でそれを実行する必要があります。 For more information, see [How to Create and Update model elements](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

### <a name="writing-the-code-of-the-methods"></a>メソッドのコードの記述
 次のコード片はこれらのメソッド内で頻繁に役立ちます。

- `this.CurrentSelection`. ユーザーが右クリックした図形は常にこの図形およびコネクタの一覧に含まれます。 ユーザーが図の空白部分をクリックした場合、このリストのメンバーは図のみになります。

- `this.IsDiagramSelected()` - `true` if the user clicked a blank part of the diagram.

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()` - ユーザーは複数の図形を選択しませんでした

- `this.SingleSelection` - ユーザーが右クリックした図形または図

- `shape.ModelElement as MyLanguageElement` - 図形により表されるモデル要素。

  For more information about how to navigate from element to element and about how to create objects and links, see [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md).

## <a name="see-also"></a>参照
 <xref:System.ComponentModel.Design.MenuCommand> [Writing Code to Customise a Domain-Specific Language](../modeling/writing-code-to-customise-a-domain-specific-language.md) [How to: Add a Command to the Shortcut Menu](../modeling/how-to-add-a-command-to-the-shortcut-menu.md) [Walkthrough: Getting Information from a Selected Link](../misc/walkthrough-getting-information-from-a-selected-link.md) [How VSPackages Add User Interface Elements](../extensibility/internals/how-vspackages-add-user-interface-elements.md) [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) [VSCT XML Schema Reference](../extensibility/vsct-xml-schema-reference.md)
