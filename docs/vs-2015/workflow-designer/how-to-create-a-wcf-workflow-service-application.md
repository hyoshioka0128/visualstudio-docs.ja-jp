---
title: '方法: WCF ワークフローサービスアプリケーションを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 12d675ac-27d8-4d86-ba16-6f7688f8c841
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9bf941babd943c6856809a13de847b62745b2056
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72605013"
---
# <a name="how-to-create-a-wcf-workflow-service-application"></a>WCF ワークフロー サービス アプリケーションを作成する方法
[!INCLUDE[indigo1](../includes/indigo1-md.md)] ワークフロー サービス アプリケーションは、そのクライアントとの間でプロセスの境界を越えてメッセージを受け渡しする分散型の通信サービスです。 サービス側でのサービス コントラクトの実装は、.NET Framework 3.5 の従来のワークフロー サービスと同様に、[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] のワークフロー アクティビティを介して宣言形式で行います。

### <a name="to-create-a-wcf-workflow-service-application"></a>WCF ワークフロー サービス アプリケーションを作成するには

1. [!INCLUDE[vs2010](../includes/vs2010-md.md)]を起動します。

2. [ **ファイル** ] メニューの [ **新規作成**] をポイントし、[ **プロジェクト**] をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. [**インストールされたテンプレート**] ペインで、選択した言語に応じて、 **Visual C#** または**Visual Basic**グループから [ **WCF** ] または [**ワークフロー** ] を選択します。

4. 中央のペインで、[ **WCF ワークフローサービスアプリケーション**] を選択します。

5. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

6. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

7. [ **ソリューション** ] ボックスで、新しいソリューションを作成するか、[ **OK]** をクリックします。

    > [!NOTE]
    > ワークフローコンソールアプリケーションを既存のソリューションに追加する場合は、でそのソリューションを開き [!INCLUDE[vs2010](../includes/vs2010-md.md)] 、**ソリューションエクスプローラー**でソリューションを右クリックして、[**追加**]、[**新しいプロジェクト...** ] の順に選択します。 を選択すると、[ **新しいプロジェクト** ] ダイアログボックスが開きます。 上記の手順を実行します。

8. プロジェクト テンプレートによって、サービス定義が XAML として作成されます。 [!INCLUDE[wfd1](../includes/wfd1-md.md)]のデザイン ビューが開かれ、<xref:System.Activities.Statements.Sequence> と <xref:System.ServiceModel.Activities.Receive> のアクティビティを含む <xref:System.ServiceModel.Activities.SendReply> アクティビティが表示されます。

## <a name="see-also"></a>参照
 方法:[ワークフロープロジェクトを作成](../workflow-designer/creating-a-workflow-project.md)する[アクティビティを作成する](https://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)