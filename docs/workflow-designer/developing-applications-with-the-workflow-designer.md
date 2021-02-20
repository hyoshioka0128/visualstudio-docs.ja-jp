---
title: ワークフロー デザイナーを使用したアプリケーションの開発
description: ワークフローデザイナーを使用してアプリケーションを開発する方法について説明します。これは、Visual Studio で WF アプリケーションをグラフィカルに構築およびデバッグするために使用できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DefaultWorkflowDesigner
- DefaultWorkflowDesigner.UI
helpviewer_keywords:
- Visual Studio Workflow Designer [WFD], overview
- Workflow Designer [WFD]
- Visual Studio Workflow Designer [WFD]
- Workflow Designer [WFD], overview
ms.assetid: 4cd062b1-b496-4668-bbc1-ee85545e066d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ee870e3c3794fc0f87b9e29e2bff8b20b79d84fa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959819"
---
# <a name="develop-apps-with-the-workflow-designer"></a>ワークフロー デザイナーでアプリを開発する

ワークフローデザイナーは、visual Studio で [Windows Workflow Foundation](/dotnet/framework/windows-workflow-foundation/index) (WF) アプリケーションをグラフィカルに構築およびデバッグするためのビジュアルデザイナーおよびデバッガーです。 テンプレートとアクティビティデザイナーを使用して、複合ワークフローアプリケーション、アクティビティライブラリ、または Windows Communication Foundation (WCF) サービスを作成できます。

## <a name="install-windows-workflow-foundation"></a>Windows Workflow Foundation のインストール

Visual Studio でワークフロープロジェクトテンプレートを使用するには、最初に **Windows Workflow Foundation** コンポーネントをインストールします。

1. Visual Studio インストーラーを開きます。 Visual Studio で **[ツール]**[  >  **ツールと機能を取得**] の順に選択すると、簡単に開くことができます。

1. Visual Studio インストーラーで、[ **個々のコンポーネント** ] タブを選択します。

1. [ **開発アクティビティ** ] カテゴリまで下へスクロールし、 **Windows Workflow Foundation** コンポーネントを選択します。

   ![Visual Studio の Windows Workflow Foundation コンポーネント](media/windows-workflow-foundation-component.png)

1. **[変更]** を選択します。

   Visual Studio によって **Windows Workflow Foundation** コンポーネントがインストールされます。

## <a name="see-also"></a>関連項目

- [Windows Workflow Foundation (.NET Framework)](/dotnet/framework/windows-workflow-foundation/index)
