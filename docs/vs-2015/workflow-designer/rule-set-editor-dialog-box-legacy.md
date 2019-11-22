---
title: Rule Set Editor Dialog Box (Legacy) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Rules.Design.RuleSetDialog.UI
helpviewer_keywords:
- Rule Set Editor dialog box
ms.assetid: 7cfd5df1-1115-4e5c-9b72-121f39419e83
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 83cdd4f549655be524abdd2a4708b316f6747b3e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302758"
---
# <a name="rule-set-editor-dialog-box-legacy"></a>[ルール セット エディター] ダイアログ ボックス (レガシ)
This topic describes how use the **Rule Set Editor** dialog box in the legacy [!INCLUDE[wfd1](../includes/wfd1-md.md)]. [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 The **Rule Set Editor** dialog box is used to create and modify [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) rule sets, which are serialized to a .rules file.

> [!NOTE]
> If you want to open the .rules file with the **XML Editor with encoding**, you must first close the associated designer window for the workflow or activity.

 For information about how to access the **Rule Set Editor** dialog box, see [How to: Create a PolicyActivity Rule Set (Legacy)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md).

> [!WARNING]
> [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする場合に使用される、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]のルール エディターは、複数バージョン対応機能をサポートしていません。

 The following table describes the user interface (UI) elements of the **Rule Set Editor** dialog box.

|UI 要素|説明|
|----------------|-----------------|
|**Add Rule**|新しいルール定義をルール セットに追加します。|
|**削除**|選択したルールをルール セットから削除します。|
|**Chaining**|ルール セットで使用するフォワード チェーンの種類を指定します。 使用可能なオプションは次のとおりです。<br /><br /> -   **Full Chaining**, which specifies to use all forward chaining mechanisms: implicit, method attributing, and explicit using an **Update** function.<br />-   **Sequential**, which specifies not to use any forward chaining.<br />-   **Explicit Update Only**, which specifies to only perform forward chaining on **Update** actions.<br /><br /> For more information about forward chaining, see [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).|
|**Name**|ルール セット リストの列見出しです。 ルール リストを名前で並べ替えるには、これをクリックします。|
|**Priority**|ルール セット リストの列見出しです。 ルール リストを優先度で並べ替えるには、これをクリックします。|
|**Reevaluation**|ルール セット リストの列見出しです。 ルール リストを再評価タイプで並べ替えるには、これをクリックします。|
|**Rule Preview**|ルール セット リストの列見出しです。 ルールの条件とアクションのプレビューでルール リストを並べ替えるには、これをクリックします。|
|**Name:**|ルールの名前を入力します。|
|**Priority:**|ルールの優先度を入力します。 既定の優先順位は 0 です。|
|**Reevaluation:**|ルールで使用するルール再評価の種類を指定します。 使用可能なオプションは次のとおりです。<br /><br /> -   **Always**, which causes the rule to be reevaluated as needed.<br />-   **Never**, which causes the rule to never be reevaluated. この場合、ルールは一度だけ実行されます。|
|**Active**|これをオンにすると、ルールはアクティブになります。|
|**Condition:**|ルールの条件式を入力します。 式の構文の詳細については、このページの「条件式とアクション式の入力」の項を参照してください。|
|**Then Actions:**|Then アクションの式を入力します。 式の構文の詳細については、このページの「条件式とアクション式の入力」の項を参照してください。|
|**Else Actions:**|Else アクションの式を入力します。 式の構文の詳細については、このページの「条件式とアクション式の入力」の項を参照してください。|
|**OK**|これをクリックすると、ルール セットが .rules ファイルに保存されます。|

 For more information about rule sets, see [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).

## <a name="entering-condition-and-action-expressions"></a>条件式とアクション式の入力
 You enter expressions for the Condition and the Then and Else actions as text in their respective text boxes in the **Rule Set Editor** dialog box. You can type **this.** into the editor to reference fields, properties and methods used in the workflow, using an IntelliSense-type of menu. または、ワークフローのメンバ名を直接入力することもできます。 クラス名とそれに続いてメソッド名を入力することにより、参照された型で静的メソッドを呼び出すことができます。

 条件には、AND、OR、NOT といった論理演算子を追加することもできます。 述語も追加できます。 述語は、バイナリ演算子と 2 つのオペランドから成ります。 The binary operators supported are ==, >, \<, >=, and <=. サポートされているオペランドは、定数値、算術関数、スコープ付きパブリック メンバです。

 You can specify the type for the comparison, and you can compare to **null** or an empty string. 複合型を含む変数でメンバに対する呼び出しをネストすることができます (たとえば `this.Address.State == "WA"`)。

 式では、次の演算子がサポートされます。

- 関係演算子 : ==、=、!=

- Comparison operators: <, \<=, >, >=

- 算術演算子 : +、-、*、/、MOD

- Logical operators: AND, &&, OR, &#124;&#124;, NOT, !

- Bitwise operators: &, &#124;

  式演算子の優先順位は、C# 演算子の優先順位規則に従います。

  For more information about conditions, see [Using Conditions in Workflows](https://msdn.microsoft.com/541211f5-d382-4810-894f-71f00b34fa77).

### <a name="halt-and-update-functions"></a>Halt 関数と Update 関数
 **Then Actions:** and **Else Actions:** expressions support **Halt** and **Update** functions. To use the **Halt** function, type **Halt** into a **Then Action:** or **Else Action:** text box. The **Halt** action causes rule set execution to stop immediately, and control returns to the calling code. You use the **Update** function with forward chaining.

 An **Update** statement can be expressed in the editor in one of two forms; both forms are shown in the following example:

```
Update(this.Address.State)
Update("this/Address/State")
```

 For more information about using **Update** with forward chaining, see [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).

## <a name="see-also"></a>参照
 [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) [Select Rule Set Dialog Box (Legacy)](../workflow-designer/select-rule-set-dialog-box-legacy.md) [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004) [Using Conditions in Workflows](https://go.microsoft.com/fwlink?LinkID=65009)