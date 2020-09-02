---
title: '方法: サービスのデータに接続する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], connecting to Web services
- data sources, creating from Web services
- data [Visual Studio], reading from Web services
- reading data, from Web services
- Web services, reading data
- Web services, as data sources
- Web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d9bfa6c776e3a2137f751d4253feb0239811d95a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72654690"
---
# <a name="how-to-connect-to-data-in-a-service"></a>方法: サービスのデータに接続する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションをサービスから返されるデータに接続するには、[データソース構成ウィザード](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)を実行し、[**データソースの種類の選択**] ページで [**サービス**] を選択します。

 ウィザードが完了すると、サービス参照がプロジェクトに追加され、[ [データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)ですぐに使用できるようになります。

> [!NOTE]
> **[データ ソース]** ウィンドウに表示される項目は、サービスから返される情報に応じて異なります。 サービスによっては、**データ ソース構成ウィザード**でバインドできるオブジェクトを作成するための十分な情報を提供しないものもあります。 たとえば、サービスが型指定されていないデータセットを返す場合、ウィザードの完了時に [ **データソース] ウィンドウ** に項目が表示されません。 これは、型指定されていないデータセットがスキーマを提供しないため、ウィザードにデータソースを作成するための十分な情報がないためです。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-connect-your-application-to-a-service"></a>アプリケーションをサービスに接続するには

1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

2. [**データソースの種類を選択**] ページで [**サービス**] を選択し、[**次へ**] をクリックします。

3. 使用するサービスのアドレスを入力するか、[ **探索** ] をクリックして現在のソリューション内のサービスを特定し、[ **移動**] をクリックします。

4. 必要に応じて、新しい **名前空間** を既定値の代わりに入力できます。

    > [!NOTE]
    > [ **詳細設定** ] をクリックして、[ [サービス参照の構成] ダイアログボックス](../data-tools/configure-service-reference-dialog-box.md)を開きます。

5. [ **OK]** をクリックして、プロジェクトにサービス参照を追加します。

6. **[完了]** をクリックします。

     **[データ ソース]** ウィンドウに、データ ソースが追加されます。

## <a name="next-steps"></a>次の手順

#### <a name="to-add-functionality-to-your-application"></a>アプリケーションに機能を追加するには

- [ **データソース** ] ウィンドウで項目を選択し、フォームにドラッグして、バインドされたコントロールを作成します。 詳細については、「 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>参照
 [Visual Studio で WCF data service Windows Communication Foundation Services および WCF Data Services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) [に WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)
