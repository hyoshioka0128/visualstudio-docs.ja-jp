---
title: '方法: Windows Communication Foundation コントラクト操作を呼び出す (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: a9058345-708f-4fcf-8739-2a43e5285b7a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6f42600a739561a27a6dd8f6caa237027bac4554
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72603699"
---
# <a name="how-to-invoke-a-windows-communication-foundation-contract-operation-legacy"></a>方法: Windows Communication Foundation コントラクト操作を呼び出す (レガシ)
このトピックでは、[!INCLUDE[indigo1](../includes/indigo1-md.md)] または [!INCLUDE[wfd1](../includes/wfd1-md.md)] を対象とする従来の [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)]を使用して [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] コントラクト操作を呼び出す方法について説明します。

 [ **Sendactivity** ] アクティビティを [ツールボックス] からワークフローデザインサーフェイスにドラッグした後、既存のコントラクトをインポートし、その **sendactivity** アクティビティから呼び出される操作を決定する必要があります。 [ [操作の選択] ダイアログボックス (レガシ)](../workflow-designer/choose-operation-dialog-box-legacy.md)を使用して、コントラクトとその操作を選択します。

 さらに、サービスで構成ファイルを使用している場合は、<xref:System.Workflow.Activities.ChannelToken> を指定する必要があります。 <xref:System.Workflow.Activities.ChannelToken> により、送信アクティビティでワークフロー サービスへの接続に使用するエンドポイント構成が特定されます。

### <a name="to-invoke-a-wcf-contract-operation-from-a-sendactivity-activity"></a>SendActivity アクティビティから WCF コントラクト操作を呼び出すには

1. デザイナーで [ **Sendactivity** ] アクティビティをダブルクリックするか、[**プロパティ**] ペインの**serviceoperationinfo**プロパティの横にある省略記号をクリックします。

2. [ **操作の選択** ] ダイアログボックスが開いたら、ダイアログボックスの右上隅にある [ **インポート** ] をクリックします。

     [ [.Net 型の参照と選択] ダイアログボックス (レガシ)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md) が開きます。

3. 必要なコントラクトを含んでいるアセンブリまたはプロジェクトを検索します。

4. コントラクトを選択し、[ **OK]** をクリックします。

5. [ **使用可能な操作**] で、呼び出す操作を選択し、[ **OK]** をクリックします。

### <a name="to-specify-a-channel-token"></a>チャネル トークンを指定するには

1. デザイナで <xref:System.Workflow.Activities.SendActivity> アクティビティを選択します。

2. [ **プロパティ** ] ペインで、の名前を指定し <xref:System.Workflow.Activities.ChannelToken> ます。 この名前は、チャネル トークンを一意に識別します。

3. チャネル トークン ノードを展開し、<xref:System.Workflow.Activities.ChannelToken.EndpointName%2A> フィールドで使用するクライアント エンドポイントの名前を指定します。 構成ファイル内の同名のエンドポイント構成が、チャネルの構成に使用されます。

4. 構成ファイル内にエンドポイント構成が存在しない場合は、エンドポイント構成を作成します。 クライアントの構成の詳細については、「 [WCF クライアントの概要](https://msdn.microsoft.com/library/f60d9bc5-8ade-4471-8ecf-5a07a936c82d)」を参照してください。

## <a name="see-also"></a>参照
 [[操作の選択] ダイアログボックス (レガシ)](../workflow-designer/choose-operation-dialog-box-legacy.md) [方法: WCF コントラクト操作 (レガシ) の](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)[レガシワークフローアクティビティ](../workflow-designer/legacy-workflow-activities.md)を実装する