---
title: '方法: PolicyActivity 規則セットを作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- PolicyActivity activity, creating rule sets
- Rule Set Editor dialog box
- PolicyActivity activity, selecting rule sets
- Select Rule Set dialog box
- rule sets, creating for PolicyActivity
ms.assetid: f272489d-3342-4511-8b59-6a0fd7a42d70
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1c18a08986bf8e4aa30969a9d30d740fb68e978c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297472"
---
# <a name="how-to-create-a-policyactivity-rule-set-legacy"></a>方法: PolicyActivity ルール セットを作成する (レガシ)
このトピックでは、[!INCLUDE[wfd1](../includes/wfd1-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする従来の [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用してポリシー アクティビティのルール セットを作成する方法について説明します。

 **ツールボックス**からワークフローデザインサーフェイスに**ポリシー**アクティビティ項目をドラッグした後、 [policyactivity](https://go.microsoft.com/fwlink?LinkID=65019)アクティビティに対して既存の規則を選択するか、新しい規則セットを作成することができます。 [ルール[セットの選択] ダイアログボックス (レガシ)](../workflow-designer/select-rule-set-dialog-box-legacy.md)を使用して既存のルールセットを選択し、[[ルールセットエディター] ダイアログボックス (レガシ)](../workflow-designer/rule-set-editor-dialog-box-legacy.md)を使用してルールセットを作成します。

> [!NOTE]
> [[ルールセットエディター] ダイアログボックス (レガシ)](../workflow-designer/rule-set-editor-dialog-box-legacy.md)ダイアログボックスは、ワークフローデザインサーフェイス上の[policyactivity](https://go.microsoft.com/fwlink?LinkID=65019)アクティビティをダブルクリックして直接開くことができます。

### <a name="to-select-or-create-a-rule-set-for-a-policyactivity-activity"></a>PolicyActivity アクティビティ用のルール セットを選択または作成するには

1. [Policyactivity](https://go.microsoft.com/fwlink?LinkID=65019)を右クリックし、 **[プロパティ]** をクリックして、 **[プロパティ]** ウィンドウを開きます。

2. **[Rulesetreference]** プロパティをクリックします。

3. 以下のいずれかを実行します。

    - **Rulesetreference**の省略記号 **[...]** をクリックし、[[ルールセットの選択] ダイアログボックス (レガシ)](../workflow-designer/select-rule-set-dialog-box-legacy.md)で既存のルールセットを選択します。 次に、手順 10. に進みます。

         または

    - ルール セットの名前を入力します。 **Rulesetreference**の省略記号 **[...]** をクリックし、[[ルールセットの選択] ダイアログボックス (レガシ)](../workflow-designer/select-rule-set-dialog-box-legacy.md)で **[編集]** を選択します。

         または

    - ルール セットの名前を入力します。 **Rulesetreference**プロパティを展開し、 **[ルールセットの定義]** プロパティの省略記号ボタン **[...]** を選択します。

         [[ルールセットエディター] ダイアログボックス (レガシ)](../workflow-designer/rule-set-editor-dialog-box-legacy.md)が開きます。

4. [[ルールセットエディター] ダイアログボックス (レガシ)](../workflow-designer/rule-set-editor-dialog-box-legacy.md)で、 **[ルールの追加]** をクリックして新しいルールをルールセットに追加します。

5. **[名前]** 、 **[優先度]** 、再 **[評価]** の各プロパティを入力するか、既定値のままにします。

6. **条件**のテキストを入力します。

7. **Then アクション**と**Else アクション**のテキストを入力します。

8. 別のルールを追加するには、 **[ルールの追加]** を再度クリックします。

9. 終了したら **[OK]** をクリックします。

## <a name="see-also"></a>関連項目
 [Policyactivity](https://go.microsoft.com/fwlink?LinkID=65019)の[[ルールセットの選択] ダイアログボックス](../workflow-designer/select-rule-set-dialog-box-legacy.md)(レガシ)[ポリシーアクティビティの](https://go.microsoft.com/fwlink?LinkID=65004)[レガシワークフローアクティビティ](../workflow-designer/legacy-workflow-activities.md)を使用する (レガシ)[ルールセットエディターダイアログボックス](../workflow-designer/rule-set-editor-dialog-box-legacy.md)