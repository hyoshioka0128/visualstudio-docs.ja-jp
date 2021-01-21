---
title: ワークフロー デザイナーで検索を使用する方法
description: ワークフローデザイナー内で検索して、キーワードによって項目を検索する方法について説明します。これにより、より大規模で複雑なワークフローを簡単に作成できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f42d3115-2ed2-4941-8f1e-92dac41c30fa
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3dadaf6ce4728dfac8d4052804cbed70ee7cefcd
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437906"
---
# <a name="how-to-use-search-in-the-workflow-designer"></a>ワークフロー デザイナーで検索を使用する方法

より大規模で複雑なワークフローの作成を容易にするために、ワークフローデザイナー内で検索して、キーワードによって項目を検索することができます。 デザイナーでは、置換はサポートされないことに注意してください。

## <a name="quick-find"></a>クイック検索

クイック検索では、デザイナーで次のものが検索されます。

- <xref:System.Activities.Activity> オブジェクト、<xref:System.Activities.Statements.FlowNode> オブジェクト、<xref:System.Activities.Statements.State> オブジェクト、遷移、およびその他のカスタム フロー制御項目のプロパティ。

- 変数

- 引数

- 式

### <a name="use-quick-find"></a>クイック検索を使用する

1. ワークフローデザイナーを開いた状態で、Ctrl キーを押し **ながら F** キーを押すか、[検索の **編集** ] を選択して [  >  **Find and Replace**  >  **クイック検索** ] をクリックします。

2. [検索する **文字列** ] ボックスに検索語句を入力し、[ **次を検索** ] をクリックします。

3. 検索用語は、現在のワークフローにあります。 次の図は、デザイナーに配置されているアクティビティの表示名を示しています。

   ![ワークフロー デザイナーでの検索結果](../workflow-designer/media/designersearch.png)

## <a name="find-in-files"></a>フォルダーを指定して検索する

[フォルダーを検索] XAML ファイルを含むワークフローファイル内の文字列を検索します。

### <a name="use-find-in-files"></a>フォルダーを使用して検索

1. Visual Studio で、 **Ctrl** + **Shift** + **F** キーを押すか、[検索の **編集** ] を選択して [フォルダーを選択して検索] をクリックし  >  **Find and Replace**  >  **Find in Files** ます。

2. [検索する **文字列** ] ボックスに検索項目を入力し、[ **すべて検索** ] をクリックします。

3. 検索結果は、[ **検索結果** ] ビューに表示されます。 結果項目をダブルクリックすると、ワークフローデザイナーでの一致を含むアクティビティに移動します。