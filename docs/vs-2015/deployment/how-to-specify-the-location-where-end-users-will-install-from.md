---
title: '方法: エンドユーザーがインストールする場所を指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 82181d906adc3454dfe77ef4fb21d8bdf99df16f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77557989"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>方法: エンド ユーザーがインストールを開始する場所を指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションを発行するときに [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、ユーザーがアプリケーションをダウンロードしてインストールする場所は、必ずしもアプリケーションを最初に発行する場所とは限りません。 たとえば、一部の組織では、開発者がアプリケーションをステージングサーバーに発行した後、管理者がアプリケーションを Web サーバーに移動する場合があります。  
  
 この場合、プロパティを使用して、 `Installation URL` ユーザーがアプリケーションをダウンロードする Web サーバーを指定できます。 これは、アプリケーションマニフェストが更新プログラムを検索する場所を認識できるようにするために必要です。  
  
 プロパティは、 `Installation URL` **プロジェクトデザイナー**の [**発行**] ページで設定できます。  
  
 **メモ** プロパティは、 `Installation URL` **publishwizard**を使用して設定することもできます。 詳細については、「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。  
  
### <a name="to-specify-an-installation-url"></a>インストール URL を指定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [インストール URL] フィールドに、形式を使用した完全修飾 URL `https://www.contoso.com/ApplicationName` または形式の UNC パスを使用して、インストール先を入力し `\\Server\ApplicationName` ます。  
  
## <a name="see-also"></a>参照  
 [方法: Visual Studio がファイルをコピーする場所を指定する](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
