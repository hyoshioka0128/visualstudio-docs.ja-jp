---
title: '方法: ClickOnce アプリケーションの [スタート] メニューの名前を指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Start menu resource name
- Start menu name
- ClickOnce deployment, Start menu name
ms.assetid: 4b5183b2-2fd4-4433-9310-4a73bb12c4e3
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 30bb4050399bf7a6d9120f7e5454b26ce505af35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149761"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>方法 : ClickOnce アプリケーションのスタート メニューの名前を指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションがオンラインとオフラインの両方でインストールされると、[**スタート**] メニューと [**プログラムの追加と削除**] の一覧にエントリが追加されます。 既定では、表示名はアプリケーションアセンブリの名前と同じですが、[**発行オプション**] ダイアログボックスの [**製品名**] を設定して表示名を変更できます。  
  
 [publish.htm] ページに**製品名**が表示されます。インストールされているオフラインアプリケーションの場合は、[**スタート**] メニューのエントリの名前になり、[**プログラムの追加と削除**] に表示される名前になります。  
  
 **発行者名** は、[publish.htm] ページの [ **製品名**] の上に表示されます。インストールされているオフラインアプリケーションの場合は、[ **スタート** ] メニューにアプリケーションのアイコンが含まれているフォルダーの名前にもなります。  
  
 [**発行オプション**] ダイアログボックスでは、[**製品名**] プロパティと [発行**元名**] プロパティを設定できます。このダイアログボックスは、**プロジェクトデザイナー**の [**発行**] ページで使用できます。  
  
### <a name="to-specify-a-start-menu-name"></a>[スタート] メニューの名前を指定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。  
  
4. [ **説明**] をクリックします。  
  
5. [ **発行オプション** ] ダイアログボックスで、[ **製品名**] に表示する名前を入力します。  
  
6. 必要に応じて、[ **発行者名**] に発行者名を入力できます。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
