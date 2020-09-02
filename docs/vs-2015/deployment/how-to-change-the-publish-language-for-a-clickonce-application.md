---
title: '方法: ClickOnce アプリケーションの発行言語を変更する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish language property
- ClickOnce deployment, changing publish language
- publishing, ClickOnce
ms.assetid: ef5024c4-cda1-4970-bc75-32a2a10c92c3
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 26e4074b731dad44cd9eed40f1c1cc755d786562
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683787"
---
# <a name="how-to-change-the-publish-language-for-a-clickonce-application"></a>方法 : ClickOnce アプリケーションの発行言語を変更する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションを公開する場合 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、インストール時に表示されるユーザーインターフェイスは、既定で開発用コンピューターの言語とカルチャになります。 ローカライズされたアプリケーションを発行する場合、ローカライズされたバージョンと一致する言語とカルチャを指定する必要があります。 これは、プロジェクトのプロパティによって決定され `Publish language` ます。  
  
 `Publish language`プロパティは、**プロジェクトデザイナー**の [**発行**] ページからアクセスできる [**発行オプション**] ダイアログボックスで設定できます。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-change-the-publish-language"></a>発行言語を変更するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。  
  
4. [ **説明**] をクリックします。  
  
5. [ **発行オプション** ] ダイアログボックスで、[ **発行言語** ] ドロップダウンリストから言語とカルチャを選択し、[ **OK**] をクリックします。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
