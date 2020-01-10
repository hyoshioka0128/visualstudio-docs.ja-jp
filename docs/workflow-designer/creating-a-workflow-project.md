---
title: Workflow Foundation プロジェクトを作成する
ms.date: 06/25/2018
ms.topic: conceptual
helpviewer_keywords:
- Workflow Designer, creating a workflow project
- creating a workflow project
ms.assetid: 235a125e-ebe7-4a98-bf77-86c8558728fb
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8c3e4930376d2d2f9a6ee3334d8b164279d5ac2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597075"
---
# <a name="workflow-project-templates"></a>ワークフロープロジェクトテンプレート

ワークフロー、Windows Communication Foundation (WCF) ワークフローサービス、カスタムアクティビティ、およびカスタムアクティビティデザイナーは、Visual Studio プロジェクトテンプレートを使用して作成できます。 この記事では、Visual Studio で使用できるプロジェクトテンプレートを使用してライブラリとアプリケーションを作成する方法について説明します。

## <a name="create-a-workflow-project"></a>ワークフロー プロジェクトを作成する

Visual Studio には、次の4つの異なるワークフロープロジェクトテンプレートが用意されています。

- ワークフローコンソールアプリ

- WCF ワークフローサービスアプリ

- 活動ライブラリ

- アクティビティデザイナーライブラリ

これらのテンプレートにアクセスするには、最初に Visual Studio の**Windows Workflow Foundation**コンポーネントをインストールします。 詳細については、「 [Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

1. **Windows Workflow Foundation**コンポーネントをインストールしたら、[**ファイル** > **新しい** > **プロジェクト**] を選択します。

1. ワークフロープロジェクトテンプレート (**ワークフローコンソールアプリケーション**テンプレートなど) を検索して選択します。

1. 続行してプロジェクトを作成します。

   > [!NOTE]
   > 既存のソリューションに新しいプロジェクトを追加する場合は、Visual Studio でそのソリューションを開き、**ソリューションエクスプローラー**でソリューションを右クリックして、[ > **新しいプロジェクト**の**追加**] を選択します。

## <a name="workflow-console-app"></a>ワークフローコンソールアプリ

**ワークフローコンソールアプリケーション**テンプレートを選択すると、Visual Studio によって XAML にワークフロー定義が作成されます。 ワークフローデザイナーが開き、作成したワークフローのキャンバスが表示されます。 ワークフローを作成するには、 **[ツールボックス]** からアクティビティまたはその他のワークフローアイテムをデザイン画面にドラッグします。

## <a name="wcf-workflow-service-app"></a>WCF ワークフローサービスアプリ

**WCF ワークフローサービスアプリケーション**テンプレートを選択すると、Visual Studio によってサービス定義が XAML として作成されます。 ワークフローデザイナーは、<xref:System.ServiceModel.Activities.Receive> と <xref:System.ServiceModel.Activities.SendReply> のアクティビティのセットを含む <xref:System.Activities.Statements.Sequence> アクティビティを含むデザインビューに表示されます。

## <a name="activity-library"></a>活動ライブラリ

**[アクティビティライブラリ]** テンプレートを選択すると、Visual Studio によって XAML にアクティビティ定義が作成されます。 ワークフローデザイナーが開き、カスタムアクティビティのキャンバスが表示されます。 アクティビティを **[ツールボックス]** からデザイン画面にドラッグして、カスタムアクティビティに追加します。

> [!NOTE]
> カスタムアクティビティの本文で使用できる子アクティビティは1つだけです。 ただし、その子アクティビティは、<xref:System.Activities.Statements.Sequence> アクティビティや <xref:System.Activities.Statements.Flowchart> アクティビティなどの複合アクティビティである可能性があります。

## <a name="activity-designer-library"></a>アクティビティデザイナーライブラリ

**アクティビティデザイナーライブラリ**テンプレートを選択すると、Visual Studio によって、アクティビティデザイナー定義が XAML と分離コード実装ファイルに作成されます。 ワークフローデザイナーが開き、アクティビティデザイナーのキャンバスが表示されます。 **ツールボックス**から WINDOWS PRESENTATION FOUNDATION (WPF) コントロールをデザイン画面にドラッグして、カスタムアクティビティデザイナーで使用できるようにします。

カスタムアクティビティデザイナーを実装する方法の例については、「[方法: カスタムアクティビティデザイナーを作成](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)する」を参照してください。

> [!NOTE]
> カスタムアクティビティデザイナーは、カスタムアクティビティおよび既定の .NET アクティビティに使用できます。

## <a name="see-also"></a>関連項目

- [ワークフローデザイナーを使用する](developing-applications-with-the-workflow-designer.md)
- [ワークフローの設計 (.NET Framework)](/dotnet/framework/windows-workflow-foundation/designing-workflows)
