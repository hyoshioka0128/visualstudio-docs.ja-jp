---
title: '方法: ClickOnce のオフラインまたはオンラインのインストールモードを指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, specifying install mode
- install mode
- online applications
- offline applications
- ClickOnce install mode
ms.assetid: 0aee5fc1-e966-4bda-9b8f-d9997aeaa779
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d4111ca5aee4a405a4a797dbfee14a3d4b50435f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149754"
---
# <a name="how-to-specify-the-clickonce-offline-or-online-install-mode"></a>方法: ClickOnce のオフラインまたはオンラインのインストール モードを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションのは、 `Install Mode` [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションがオフラインでもオンラインでも利用できるかどうかを決定します。 [アプリケーションを **オンラインでのみ利用可能**にする] を選択した場合、ユーザーは [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを実行するために、発行場所 (Web ページまたはファイル共有) にアクセスできる必要があります。 [アプリケーションを **オフラインでも使用できる**] を選択すると、アプリケーションによって [ **スタート** ] メニューと [ **プログラムの追加と削除** ] ダイアログボックスにエントリが追加されます。ユーザーは、接続されていないときにアプリケーションを実行できます。  
  
 は、 `Install Mode` **プロジェクトデザイナー**の [**発行**] ページで設定できます。  
  
 **メモ** は、 `Install Mode` 発行ウィザードを使用して設定することもできます。 詳細については、「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。  
  
### <a name="to-make-a-clickonce-application-available-online-only"></a>ClickOnce アプリケーションをオンラインでのみ使用できるようにするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **インストールモードと設定** ] 領域で、[ **アプリケーションはオンラインのみで利用可能** ] オプションボタンをクリックします。  
  
### <a name="to-make-a-clickonce-application-available-online-or-offline"></a>ClickOnce アプリケーションをオンラインまたはオフラインで使用できるようにするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **インストールモードと設定** ] 領域で、[ **アプリケーションはオフラインでも利用でき** ます] オプションボタンをクリックします。  
  
     アプリケーションをインストールすると、[ **スタート** ] メニューと [コントロールパネル] の [ **プログラムの追加と削除** ] にエントリが追加されます。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
