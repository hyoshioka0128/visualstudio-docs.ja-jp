---
title: '[発行] ページの指定 (ClickOnce アプリ)'
description: プロジェクトの [発行ページ] プロパティを設定する方法について説明します。これにより、ClickOnce アプリケーションの Web ページを指定できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying publish page
- Publish Page property
- publishing, ClickOnce
- ClickOnce deployment, specifying publish page
ms.assetid: 9d70eebb-bdee-4b42-8e7e-7a07e199bdf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f58b7d8d4244f7c429c3866bf76c514bf24164ff
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940450"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションの発行ページを指定する
アプリケーションを発行すると [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、既定の Web ページ (publish.htm) が生成され、アプリケーションと共に発行されます。 このページには、アプリケーションの名前、アプリケーションをインストールするためのリンク、前提条件、およびを説明するヘルプトピックへのリンクが表示され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 プロジェクトの [ **発行ページ]** プロパティを使用すると、アプリケーションの Web ページの名前を指定でき [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

 [発行] ページが指定されると、次に発行するときに、発行場所にコピーされます。再発行すると、上書きされません。 ページの外観をカスタマイズする場合は、変更内容が失われないようにする必要があります。 詳細については、「 [方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)」を参照してください。

 [発行]**ページ** のプロパティは、**プロジェクトデザイナー** の [**発行**] ペインからアクセスできる [**発行オプション**] ダイアログボックスで設定できます。

### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>ClickOnce アプリケーションのカスタム Web ページを指定するには

1. **ソリューションエクスプローラー** でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。

2. [ **発行** ] ペインを選択します。

3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。

4. **[デプロイ]** をクリックします。

5. [ **発行オプション** ] ダイアログボックスで、[ **発行後に配置 Web ページを開く** ] チェックボックスがオンになっていることを確認します (既定ではオンになっています)。

6. [ **配置 web ページ** ] ボックスに web ページの名前を入力し、[ **OK**] をクリックします。

### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>発行するたびに発行ページが起動されないようにするには

1. **ソリューションエクスプローラー** でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。

2. [ **発行** ] ペインを選択します。

3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。

4. **[デプロイ]** をクリックします。

5. [ **発行オプション** ] ダイアログボックスで、[ **発行後に配置 Web ページを開く** ] チェックボックスをオフにします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)