---
title: '方法: ClickOnce アプリケーションの発行ページを指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 63356c6eb423ddead54290cc11c865a5102f55f2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202164"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>方法 : ClickOnce アプリケーションの発行ページを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションを発行すると [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、既定の Web ページ (publish.htm) が生成され、アプリケーションと共に発行されます。 このページには、アプリケーションの名前、アプリケーションをインストールするためのリンク、前提条件、およびを説明するヘルプトピックへのリンクが表示され [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 プロジェクトの [ **発行ページ]** プロパティを使用すると、アプリケーションの Web ページの名前を指定でき [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。  
  
 [発行] ページが指定されると、次に発行するときに、発行場所にコピーされます。再発行すると、上書きされません。 ページの外観をカスタマイズする場合は、変更内容が失われないようにする必要があります。 詳細については、「 [方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)」を参照してください。  
  
 [発行]**ページ**のプロパティは、**プロジェクトデザイナー**の [**発行**] ペインからアクセスできる [**発行オプション**] ダイアログボックスで設定できます。  
  
### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>ClickOnce アプリケーションのカスタム Web ページを指定するには  
  
1. **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。  
  
2. [ **発行** ] ペインを選択します。  
  
3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。  
  
4. **[デプロイ]** をクリックします。  
  
5. [ **発行オプション** ] ダイアログボックスで、[ **発行後に配置 Web ページを開く** ] チェックボックスがオンになっていることを確認します (既定ではオンになっています)。  
  
6. [ **配置 web ページ** ] ボックスに web ページの名前を入力し、[ **OK**] をクリックします。  
  
### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>発行するたびに発行ページが起動されないようにするには  
  
1. **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。  
  
2. [ **発行** ] ペインを選択します。  
  
3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。  
  
4. **[デプロイ]** をクリックします。  
  
5. [ **発行オプション** ] ダイアログボックスで、[ **発行後に配置 Web ページを開く** ] チェックボックスをオフにします。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)
