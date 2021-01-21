---
title: '方法: サービスのデータに接続する'
description: データソース構成ウィザードを実行し、[データソースの種類の選択] ページで [サービス] を選択して、サービスから返されたデータにアプリを接続します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting to web services
- data sources, creating from web services
- data [Visual Studio], reading from web services
- reading data, from web services
- web services, reading data
- web services, as data sources
- web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3c565f7238edf9126dd651fa567de82aed7b8d21
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94435014"
---
# <a name="how-to-connect-to-data-in-a-service"></a>方法: サービスのデータに接続する

アプリケーションをサービスから返されるデータに接続するには、 [データソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を実行し、[ **データソースの種類の選択** ] ページで [ **サービス** ] を選択します。

ウィザードが完了すると、サービス参照がプロジェクトに追加され、[ [データソース] ウィンドウ](add-new-data-sources.md#data-sources-window)ですぐに使用できるようになります。

> [!NOTE]
> **[データ ソース]** ウィンドウに表示される項目は、サービスから返される情報に応じて異なります。 サービスによっては、 **データ ソース構成ウィザード** でバインドできるオブジェクトを作成するための十分な情報を提供しないものもあります。 たとえば、サービスが型指定されていないデータセットを返す場合、ウィザードの完了時に [ **データソース** ] ウィンドウに項目が表示されません。 これは、型指定されていないデータセットがスキーマを提供しないため、ウィザードにデータソースを作成するための十分な情報がないためです。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-connect-your-application-to-a-service"></a>アプリケーションをサービスに接続するには

1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

2. [ **データソースの種類を選択** ] ページで [ **サービス** ] を選択し、[ **次へ** ] をクリックします。

3. 使用するサービスのアドレスを入力するか、[ **探索** ] をクリックして現在のソリューション内のサービスを特定し、[ **移動** ] をクリックします。

4. 必要に応じて、既定値の代わりに新しい **名前空間** を入力することもできます。

    > [!NOTE]
    > [ **詳細設定** ] をクリックして、[ [サービス参照の構成] ダイアログボックス](../data-tools/configure-service-reference-dialog-box.md)を開きます。

5. [ **OK]** をクリックして、プロジェクトにサービス参照を追加します。

6. **[完了]** をクリックします。

     **[データ ソース]** ウィンドウに、データ ソースが追加されます。

## <a name="next-steps"></a>次のステップ

アプリケーションに機能を追加するには、[ **データソース** ] ウィンドウで項目を選択し、フォームにドラッグして、バインドされたコントロールを作成します。 詳細については、「 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [WCF Data Service への WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)
- [Visual Studio での Windows Communication Foundation Services と WCF data services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
