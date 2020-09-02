---
title: '方法: ClickOnce の発行バージョンを自動的にインクリメントする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], incrementing publish version automatically
- Publish Version property, incrementing
- ClickOnce deployment, incrementing publish version automatically
- publishing, ClickOnce
ms.assetid: 686ab88a-6305-4914-a05b-fe269cc0ae1e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 50faf70e8eda6ef7ab01201102540729497eb87b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683923"
---
# <a name="how-to-automatically-increment-the-clickonce-publish-version"></a>方法 : ClickOnce の発行バージョンを自動的にインクリメントする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションを公開するときに、プロパティを変更すると、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] `Publish Version` アプリケーションが更新プログラムとして発行されます。 既定では、アプリケーションを発行するたびに、Visual Studio によっての数が自動的に増加し `Revision` `Publish Version` ます。  
  
 この動作は、**プロジェクトデザイナー**の [**発行**] ページで無効にすることができます。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-disable-automatically-incrementing-the-publish-version"></a>発行バージョンを自動的にインクリメントしないようにするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **発行バージョン** ] セクションで、[ **リリースごとにリビジョンを自動的にインクリメント** する] チェックボックスをオフにします。  
  
## <a name="see-also"></a>参照  
 [方法: ClickOnce の発行バージョンを設定する](../deployment/how-to-set-the-clickonce-publish-version.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
