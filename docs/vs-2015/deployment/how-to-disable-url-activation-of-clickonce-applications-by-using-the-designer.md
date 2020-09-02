---
title: '方法: デザイナーを使用して ClickOnce アプリケーションの URL アクティベーションを無効にする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowURLActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: a337a582-e67c-409a-b52e-607cd1a8fc57
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 27690ab275d0c7ef2a090fa8ef2e42887ae9daeb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153811"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer"></a>方法 : デザイナーを使用して ClickOnce アプリケーションの URL アクティベーションを無効にする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、アプリケーションは、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] Web サーバーからインストールされた直後に自動的に起動します。 セキュリティ上の理由から、この動作を無効にし、代わりに [ **スタート** ] メニューからアプリケーションを起動するようにユーザーに指示することができます。 次の手順では、URL アクティベーションを無効にする方法を説明します。  
  
 この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションにのみ使用できます。 オンライン専用アプリケーションでは使用できません。このアプリケーションは、URL を使用してのみ開始できます。 オンラインのみのアプリケーションとインストールされているアプリケーションの違いの詳細については、「 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。  
  
 この手順では [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、を使用します。 このタスクは、を使用して実行することもでき [!INCLUDE[winsdklong](../includes/winsdklong-md.md)] ます。 詳細については、「 [方法: ClickOnce アプリケーションの URL アクティベーションを無効](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)にする」を参照してください。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには  
  
1. **ソリューションエクスプローラー**でプロジェクト名を右クリックし、[**プロパティ**] をクリックします。  
  
2. [ **プロパティ** ] ページで、[ **発行** ] タブをクリックします。  
  
3. **[オプション]** をクリックします。  
  
4. [ **マニフェスト**] をクリックします。  
  
5. [ **ブロックアプリケーションが URL 経由でアクティブ化され**ないようにする] チェックボックスをオンにします。  
  
6. アプリケーションをデプロイします。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
