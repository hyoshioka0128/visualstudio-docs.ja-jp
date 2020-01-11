---
title: 従来のアクティビティデザイナーを使用する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- activities, configuring
- custom activities
- Activity Designer
- child activities, adding
- activities, adding child
- activities, creating custom
ms.assetid: 2fea8a05-6e58-423d-94bf-a822b15ffb80
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cd8d18d95fabd858354c625d2c9b32459efc7193
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846154"
---
# <a name="using-the-legacy-activity-designer"></a>従来のアクティビティ デザイナーの使用
このトピックでは、従来の [!INCLUDE[wfd1](../includes/wfd1-md.md)]でアクティビティ デザイナーを使用する方法について説明します。 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] または [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] を対象とする場合は、従来のデザイナーを使用します。

 アクティビティ デザイナーを使用すると、独自のカスタム アクティビティを作成できます。

## <a name="creating-a-custom-activity"></a>カスタム アクティビティの作成
 アクティビティ デザイナを使ってカスタム アクティビティを作成するには、次の手順に従います。

1. **[プロジェクト]** メニューの **[アクティビティの追加]** をクリックします。

2. **アクティビティ**または**アクティビティ (コード分離付き)** テンプレートを選択します。

   1. **アクティビティテンプレートを**使用して、同じコードファイルにアクティビティ定義とユーザーコードを持つアクティビティを作成します。

   2. アクティビティ定義がワークフローマークアップとして表現され、ユーザーコードが別のコードファイルに含まれるアクティビティを作成するには、**アクティビティ (コード分離付き)** テンプレートを使用します。

3. アクティビティ名を入力するか、既定の名前をそのままにして、 **[追加]** をクリックします。

   また、" **Workflow Activity Library**" という種類の新しいプロジェクトを作成して、カスタムアクティビティのセットを作成することもできます。 このプロジェクトの種類の詳細については、「[方法: ワークフローアクティビティライブラリを作成する (レガシ)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md)」を参照してください。

## <a name="configuring-an-activity"></a>アクティビティの構成
 アクティビティ デザイナがアクティブであるときに、プロパティ ブラウザを使用すると、次の表にリストされているプロパティを構成できます。

|property|コメント|
|--------------|--------------|
|**名前**|アクティビティの名前。|
|**基本クラス**|アクティビティの派生元の基本クラス。 既定の基底クラスは[Sequenceactivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequenceactivity.aspx)です。 **[プロパティ]** ウィンドウで、**基本クラス**の省略記号 **[...]** をクリックして、[ [.net 型の参照と選択] ダイアログボックス (レガシ)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md)で別の基本クラスを選択します。|
|**説明**|アクティビティに関するユーザー定義の説明。|
|**Enabled**|アクティビティの実行と検証を有効にするには、既定で**True**に設定します。 アクティビティの実行と検証を無効にするには、 **False**に設定します。 アクティビティの実行と検証の詳細については、「[ワークフローアクティビティの開発](https://msdn2.microsoft.com/library/ms734413.aspx)」を参照してください。|

## <a name="adding-child-activities"></a>子アクティビティの追加
 子アクティビティを、ツールボックスから設計中のアクティビティまでドラッグすることができます。 その後、プロパティ ブラウザを使ってそれぞれの子アクティビティを構成できます。

## <a name="see-also"></a>参照
 [ワークフローアクティビティの開発](https://msdn2.microsoft.com/library/ms734413.aspx)[カスタムアクティビティの作成](https://msdn2.microsoft.com/library/bb675228.aspx)[従来のワークフローアクティビティ](../workflow-designer/legacy-workflow-activities.md)[カスタムアクティビティのサンプル](https://msdn2.microsoft.com/library/bb472471.aspx)方法:[従来のワークフローデザイナーを使用して](../workflow-designer/using-the-legacy-workflow-designer.md)[ワークフローアクティビティライブラリ (レガシ) を作成する](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md)
