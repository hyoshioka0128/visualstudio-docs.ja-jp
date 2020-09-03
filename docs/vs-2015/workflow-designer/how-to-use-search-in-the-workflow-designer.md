---
title: '方法: ワークフローデザイナーで検索を使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: f42d3115-2ed2-4941-8f1e-92dac41c30fa
caps.latest.revision: 3
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 84f74b4718a7f976b386197a79692256ab49caa4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659123"
---
# <a name="how-to-use-search-in-the-workflow-designer"></a>ワークフロー デザイナーで検索を使用する方法
より大規模で複雑なワーク フローの作成を容易にするために、ワークフロー デザイナー内で検索を使用して、キーワードで項目を検索できます。 デザイナーでは、置換はサポートされないことに注意してください。 検索では、デザイナーで次の項目が検索されます。

## <a name="quick-find"></a>[クイック検索]
 クイック検索はデザイナー内で次の項目を検索します。

- <xref:System.Activities.Activity> オブジェクト、<xref:System.Activities.Statements.FlowNode> オブジェクト、<xref:System.Activities.Statements.State> オブジェクト、遷移、およびその他のカスタム フロー制御項目のプロパティ。

- 変数

- 引数

- 式

#### <a name="using-quick-find"></a>クイック検索の使用

1. ワークフローデザイナーを開いた状態で、Ctrl キーを押し **ながら F**キーを押すか、[ **編集**]、[ **検索と置換**]、[ **クイック検索**] を選択します。

2. [検索する **文字列** ] ボックスに検索語句を入力し、[ **次を検索**] をクリックします。

3. 検索用語が現在のワークフローで検索されます。 アクティビティの表示名がデザイナーで見つかったことを示すスクリーンショットを次に示します。

     ![ワークフロー デザイナーでの検索結果](../workflow-designer/media/designersearch.png "デザイナ検索")

## <a name="find-in-files"></a>フォルダーを指定して検索する
 [フォルダーを指定して検索] を使用すると、XAML ファイルなどのワークフロー ファイル内で文字列が検索されます。

#### <a name="using-find-in-files"></a>フォルダーを指定して検索の使用

1. Visual Studio で、Ctrl キーと Shift キーを押し**ながら F**キーを押すか、[**編集**]、[**検索と置換**]、[フォルダーを選択して**検索**] を選択します。

2. [検索する**文字列**] ボックスに検索項目を入力し、[**すべて検索**] をクリックします。

3. 検索結果は、[ [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] **検索結果**] ビューに表示されます。 結果の項目をダブルクリックすると、ワークフロー デザイナーで一致する項目を含むアクティビティに移動します。