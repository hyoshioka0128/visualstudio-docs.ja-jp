---
title: '方法: WCF データ サービス参照を追加、更新、または削除する'
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: c60dffc7bb47336ae36e64a366def3c4dce06213
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586589"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>方法: WCF データ サービス参照を追加、更新、または削除する
*サービス参照*を使用すると、プロジェクトは1つ以上の [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]にアクセスできます。 **[サービス参照の追加]** ダイアログボックスを使用すると、現在のソリューション内の [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]、ローカルエリアネットワーク上、またはインターネット上で検索できます。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-service-reference"></a>サービス参照の追加

### <a name="to-add-a-reference-to-an-external-service"></a>外部サービスへの参照を追加するには

1. **ソリューションエクスプローラー**で、サービスを追加するプロジェクトの名前を右クリックし、 **[サービス参照の追加]** をクリックします。

     **[サービス参照の追加]** ダイアログボックスが表示されます。

2. **アドレス** ボックスにサービスの URL を入力し、検索**をクリックし**てサービスを検索します。 サービスがユーザー名とパスワードのセキュリティを実装している場合は、ユーザー名とパスワードの入力を求められることがあります。

    > [!NOTE]
    > 信頼できるソースのサービスのみを参照してください。 信頼できないソースの参照を追加すると、セキュリティが損なわれる可能性があります。

     **アドレス**一覧から url を選択することもできます。これには、有効なサービスメタデータが見つかった前の15個の url が格納されます。

     検索が実行されると、進行状況バーが表示されます。 **[停止]** をクリックすると、いつでも検索を停止できます。

3. **サービス**の一覧で、使用するサービスのノードを展開し、エンティティセットを選択します。

4. **[名前空間]** ボックスに、参照に使用する名前空間を入力します。

5. **[OK]** をクリックして、参照をプロジェクトに追加します。

     サービスクライアント (プロキシ) が生成され、サービスを記述するメタデータが*app.config*ファイルに追加されます。

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>現在のソリューションのサービスへの参照を追加するには

1. **ソリューションエクスプローラー**で、サービスを追加するプロジェクトの名前を右クリックし、 **[サービス参照の追加]** をクリックします。

    **[サービス参照の追加]** ダイアログボックスが表示されます。

2. **[検出]** をクリックします。

    現在のソリューションのすべてのサービス ([!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] と WCF サービスの両方) が**サービス**の一覧に追加されます。

3. **サービス**の一覧で、使用するサービスのノードを展開し、エンティティセットを選択します。

4. **[名前空間]** ボックスに、参照に使用する名前空間を入力します。

5. **[OK]** をクリックして、参照をプロジェクトに追加します。

    サービスクライアント (プロキシ) によってが生成され、サービスを記述するメタデータが*app.config*ファイルに追加されます。

## <a name="update-a-service-reference"></a>サービス参照の更新
[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] の Entity Data Model が変更されることがあります。 この場合は、サービス参照を更新する必要があります。

### <a name="to-update-a-service-reference"></a>サービス参照を更新するには

- **ソリューションエクスプローラー**で、サービス参照を右クリックし、 **[サービス参照の更新]** をクリックします。

     参照が元の場所から更新されている間、進行状況を示すダイアログボックスが表示され、メタデータの変更を反映するためにサービスクライアントが再生成されます。

## <a name="remove-a-service-reference"></a>サービス参照の削除
サービス参照が使用されなくなった場合は、ソリューションから削除できます。

### <a name="to-remove-a-service-reference"></a>サービス参照を削除するには

- **ソリューションエクスプローラー**で、サービス参照を右クリックし、 **[削除]** をクリックします。

     サービスクライアントがソリューションから削除され、サービスを説明するメタデータが*app.config*ファイルから削除されます。

    > [!NOTE]
    > サービス参照を参照するコードは、手動で削除する必要があります。

## <a name="see-also"></a>関連項目

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
