---
title: '方法: ClickOnce アプリケーションの URL アクティベーションを無効にする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowUrlActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: db31a16b-960f-4264-91d7-c7c40f876068
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 75a98706858323693ec01ec3c3420a6d2d25ffef
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697224"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications"></a>方法 : ClickOnce アプリケーションの URL アクティべーションを無効にする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションは Web サーバーからインストールされた直後に自動的に起動します。 ただし、セキュリティ上の理由から、この動作を無効にすることもできます。その場合は、**[スタート]** メニューからアプリケーションを起動するようにユーザーに通知します。 次の手順では、URL アクティベーションを無効にする方法を説明します。  
  
 この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションにのみ使用できます。 URL を使用する方法でのみ起動できるオンライン専用のアプリケーションには使用できません。 オンライン専用アプリケーションとインストールされたアプリケーションの違いの詳細については、「[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。  
  
 この手順では、[!INCLUDE[winsdklong](../includes/winsdklong-md.md)] ツールである MageUI.exe を使用します。 このツールの詳細については、「 [MageUI.exe (マニフェスト生成および編集ツール、グラフィカルクライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)」を参照してください。 この手順は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用して実行することもできます。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには  
  
1. MageUI.exe で配置マニフェストを開きます。 まだ作成していない場合は、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の手順に従います。  
  
2. **[配置オプション]** タブを選択します。  
  
3. **[インストール後にアプリケーションを自動的に実行する]** チェックボックスをオフにします。  
  
4. マニフェストを保存し、署名します。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
