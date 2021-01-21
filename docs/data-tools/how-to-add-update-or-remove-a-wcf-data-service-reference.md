---
title: WCF データ サービス参照を追加、更新、または削除する
description: 「Windows Communication Foundation (WCF) データサービス参照を追加、更新、または削除する方法」を参照してください。
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 6e6c289038c3f8cb9d1586ae4a1f7a84b563239f
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436434"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>方法: WCF データ サービス参照を追加、更新、または削除する

::: moniker range="vs-2017"
*サービス参照* を使用すると、プロジェクトは1つ以上のにアクセスでき [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] ます。 [ **サービス参照の追加** ] ダイアログボックスを使用すると、 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 現在のソリューション内、ローカルエリアネットワーク上、またはインターネット上で検索できます。
::: moniker-end
::: moniker range=">=vs-2019"
**ソリューションエクスプローラー** の [ **接続済みサービス** ] ノードを使用して **Microsoft WCF Web Service Reference Provider** にアクセスできます。これにより、Windows Communication Foundation (WCF) データサービス参照を管理できます。
::: moniker-end

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-wcf-service-reference"></a>WCF サービス参照を追加する

### <a name="to-add-a-reference-to-an-external-service"></a>外部サービスへの参照を追加するには

::: moniker range="vs-2017"

1. **ソリューションエクスプローラー** で、サービスを追加するプロジェクトの名前を右クリックし、[ **サービス参照の追加** ] をクリックします。

   [ **サービス参照の追加** ] ダイアログ ボックスが表示されます。

1. [ **アドレス** ] ボックスにサービスの URL を入力し、[検索] **をクリックし** てサービスを検索します。 サービスがユーザー名とパスワードのセキュリティを実装している場合は、ユーザー名とパスワードの入力を求められることがあります。

    > [!NOTE]
    > 信頼できるソースのサービスのみを参照してください。 信頼できないソースの参照を追加すると、セキュリティが損なわれる可能性があります。

     **アドレス** 一覧から url を選択することもできます。これには、有効なサービスメタデータが見つかった前の15個の url が格納されます。

     検索が実行されると、進行状況バーが表示されます。 [ **停止** ] をクリックすると、いつでも検索を停止できます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティセットを選択します。

1. [ **名前空間** ] ボックスに、参照で使用する名前空間を入力します。

1. [ **OK** ] をクリックして、プロジェクトに参照を追加します。

     サービスクライアント (プロキシ) が生成され、サービスを記述するメタデータが *app.config* ファイルに追加されます。
::: moniker-end
::: moniker range=">=vs-2019"
1. **ソリューションエクスプローラー** で、[ **接続済みサービス** ] ノードをダブルクリックまたはタップします。

   [ **サービスの構成** ] タブが開きます。

1. [ **Microsoft WCF Web Service Reference Provider** ] を選択します。

   [ **WCF Web サービス参照の構成** ] ダイアログボックスが表示されます。

   ![[WCF Web サービスプロバイダー] ダイアログボックスのスクリーンショット](media/vs-2019/configure-wcf-web-service-reference-dialog.png)


1. [ **URI** ] ボックスにサービスの URL を入力し、[検索] **をクリックし** てサービスを検索します。 サービスがユーザー名とパスワードのセキュリティを実装している場合は、ユーザー名とパスワードの入力を求められることがあります。

    > [!NOTE]
    > 信頼できるソースのサービスのみを参照してください。 信頼できないソースの参照を追加すると、セキュリティが損なわれる可能性があります。

     [ **URI** ] ボックスの一覧から url を選択することもできます。この url には、有効なサービスメタデータが見つかった前の15個の url が格納されます。

     検索が実行されると、進行状況バーが表示されます。 [ **停止** ] をクリックすると、いつでも検索を停止できます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティセットを選択します。

1. [ **名前空間** ] ボックスに、参照で使用する名前空間を入力します。

1. [ **完了** ] をクリックして、参照をプロジェクトに追加します。

     サービスクライアント (プロキシ) が生成され、サービスを記述するメタデータが *app.config* ファイルに追加されます。

::: moniker-end

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>現在のソリューションのサービスへの参照を追加するには

::: moniker range="vs-2017"

1. **ソリューションエクスプローラー** で、サービスを追加するプロジェクトの名前を右クリックし、[ **サービス参照の追加** ] をクリックします。

    [ **サービス参照の追加** ] ダイアログ ボックスが表示されます。

1. [ **検出** ] をクリックします。

    現在のソリューションのすべてのサービス ( [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] と WCF サービスの両方) が **サービス** の一覧に追加されます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティセットを選択します。

1. [ **名前空間** ] ボックスに、参照で使用する名前空間を入力します。

1. [ **OK** ] をクリックして、プロジェクトに参照を追加します。

    サービスクライアント (プロキシ) によってが生成され、サービスを記述するメタデータが *app.config* ファイルに追加されます。
::: moniker-end
::: moniker range=">=vs-2019"
1. **ソリューションエクスプローラー** で、[ **接続済みサービス** ] ノードをダブルクリックまたはタップします。 

   [ **サービスの構成** ] タブが開きます。

1. [ **Microsoft WCF Web Service Reference Provider** ] を選択します。

   [ **WCF Web サービス参照の構成** ] ダイアログボックスが表示されます。

1. [ **検出** ] をクリックします。

    現在のソリューションのすべてのサービス ( [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] と WCF サービスの両方) が **サービス** の一覧に追加されます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティセットを選択します。

1. [ **名前空間** ] ボックスに、参照で使用する名前空間を入力します。

1. [ **完了** ] をクリックして、参照をプロジェクトに追加します。

    サービスクライアント (プロキシ) によってが生成され、サービスを記述するメタデータが *app.config* ファイルに追加されます。

::: moniker-end

## <a name="update-a-service-reference"></a>サービス参照の更新

Entity Data Model が変更される [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 場合があります。 この場合は、サービス参照を更新する必要があります。

### <a name="to-update-a-service-reference"></a>サービス参照を更新するには

- **ソリューションエクスプローラー** で、サービス参照を右クリックし、[ **サービス参照の更新** ] をクリックします。

     参照が元の場所から更新されている間、進行状況を示すダイアログボックスが表示され、メタデータの変更を反映するためにサービスクライアントが再生成されます。

## <a name="remove-a-service-reference"></a>サービス参照の削除

サービス参照が使用されなくなった場合は、ソリューションから削除できます。

### <a name="to-remove-a-service-reference"></a>サービス参照を削除するには

- **ソリューションエクスプローラー** で、サービス参照を右クリックし、[ **削除** ] をクリックします。

     サービスクライアントがソリューションから削除され、サービスを説明するメタデータが *app.config* ファイルから削除されます。

    > [!NOTE]
    > サービス参照を参照するコードは、手動で削除する必要があります。

## <a name="see-also"></a>関連項目

- [Visual Studio での Windows Communication Foundation Services と WCF data services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
