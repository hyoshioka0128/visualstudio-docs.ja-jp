---
title: '方法: ClickOnce の発行バージョンを設定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, setting publish version
- publishing, ClickOnce
- Publish Version property
ms.assetid: 06f15504-6385-40a6-b01d-cd90ca36dc73
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ec5d5d742b5a0749d1d5d52cee0a0545dd8570f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841668"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>方法: ClickOnce の発行バージョンを設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロパティは、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] `Publish Version` 発行するアプリケーションが更新プログラムとして扱われるかどうかを決定します。 バージョンがインクリメントされるたびに、アプリケーションが更新プログラムとして発行されます。  
  
 プロパティは、 `Publish Version` **プロジェクトデザイナー**の [**発行**] ページで設定できます。  
  
> [!NOTE]
> アプリケーションが発行されるたびにプロパティが自動的にインクリメントされるプロジェクトオプションがあります。 `Publish Version` このオプションは既定で有効になっています。 詳細については、「 [方法: ClickOnce の発行バージョンを自動的にインクリメント](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)する」を参照してください。  
  
### <a name="to-change-the-publish-version"></a>発行バージョンを変更するには  
  
1. **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **バージョンの発行** ] フィールドで、 **メジャー**、 **マイナー**、 **ビルド**、 **リビジョン** の各バージョン番号を増分します。  
  
    > [!NOTE]
    > バージョン番号を減らすことはできません。これを行うと、予測できない更新動作が発生する可能性があります。  
  
## <a name="see-also"></a>参照  
 [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)   
 [方法: ClickOnce の発行バージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
