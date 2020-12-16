---
title: Outlook ソリューション
description: VSTO アドインを使用して Outlook の自動化、Outlook の機能の拡張、または Outlook のユーザーインターフェイス (UI) のカスタマイズを行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], Outlook
- Office projects [Office development in Visual Studio], Outlook
- Office solutions [Office development in Visual Studio], Outlook
- templates [Office development in Visual Studio], Outlook
- projects [Office development in Visual Studio], Outlook
- Outlook [Office development in Visual Studio]
- e-mail [Office development in Visual Studio], Outlook solutions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ded4652704a47252f0839aed151f0557ae5e6766
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527550"
---
# <a name="outlook-solutions"></a>Outlook ソリューション
  Visual Studio には、Microsoft Office Outlook の VSTO アドインを作成するために使用できるプロジェクト テンプレートが用意されています。 VSTO アドインを使用して、Outlook の自動化、Outlook の機能の拡張、または Outlook のユーザー インターフェイス (UI) のカスタマイズが可能です。 VSTO アドインについて詳しくは、「 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)」をご覧ください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="create-an-outlook-vsto-add-in-project"></a>Outlook VSTO アドインプロジェクトを作成する
 Outlook プロジェクトを作成するには、 **[新しいプロジェクト]** ダイアログ ボックスにある **[Outlook アドイン]** プロジェクト テンプレートを使用します。 このテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 VSTO アドインプロジェクトを作成する方法の詳細については、「 [方法: Visual Studio で Office プロジェクトを作成](../vsto/how-to-create-office-projects-in-visual-studio.md)する」を参照してください。 プロジェクトテンプレートの詳細については、「 [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="outlook-vsto-add-in-programming-model"></a>Outlook VSTO アドインのプログラミングモデル
 Outlook VSTO アドイン プロジェクトを作成すると、 `ThisAddIn`と呼ばれる、ソリューションの基礎となるクラスが Visual Studio によって生成されます。 このクラスは、コードを記述する際の開始点となり、Outlook のオブジェクト モデルを VSTO アドインに公開します。

 `ThisAddIn`クラスおよび Vsto アドインで使用できるその他の機能の詳細については、「[プログラム vsto アドイン](../vsto/programming-vsto-add-ins.md)」を参照してください。

## <a name="automate-outlook-by-using-the-outlook-object-model"></a>Outlook オブジェクトモデルを使用した Outlook の自動化
 Outlook オブジェクト モデルでは、Outlook の自動化に使用できる型が多数公開されています。 それらの型によって、次のような一般的なタスクを実行するコードを作成できます。

- プログラムで電子メール メッセージを作成し、送信する。

- 新しい会議出席依頼を送信する。

- Outlook フォルダー内のアイテムを検索する。

  詳細については、「 [Outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)」を参照してください。

## <a name="customize-the-user-interface-of-an-outlook-application"></a>Outlook アプリケーションのユーザーインターフェイスをカスタマイズする

|タスク|詳細情報|
|----------|--------------------------|
|Outlook インスペクターのリボンにカスタム タブを追加する。|[リボンの概要](../vsto/ribbon-overview.md)|
|Outlook インスペクターの組み込みタブにカスタム グループを追加する。|[方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)|
|Outlook インスペクターに表示されるカスタム作業ウィンドウを追加する。|[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)。|
|既存の Outlook フォームを拡張または置換するフォーム領域を追加する。|[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)|

 Outlook およびその他の Microsoft Office アプリケーションの UI をカスタマイズする方法の詳細については、「 [OFFICE ui のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)|Outlook オブジェクト モデルによって提供されるオブジェクトの概要を説明します。|
|[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)|フォーム領域のデザイン、開発、およびデバッグを簡単に実行できる、Visual Studio によって提供されるツールについて説明します。|
|[チュートリアル: 初めての Outlook 用 VSTO Add-In の作成](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)|Microsoft Office Outlook 用の VSTO アドインを作成する方法について説明します。|
|[Office 開発における Outlook 2010](/previous-versions/office/developer/office-2010/ff458122(v=office.14))|この MSDN ライブラリの領域では、Outlook ソリューションの開発に関する記事やリファレンス ドキュメントを参照できます (Visual Studio を使用した Office 開発以外のトピックも含まれています)。|
