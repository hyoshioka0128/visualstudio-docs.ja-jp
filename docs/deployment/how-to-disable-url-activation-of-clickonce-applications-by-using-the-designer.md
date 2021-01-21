---
title: デザイナーを使用して ClickOnce アプリの URL アクティベーションを無効にする
description: Visual Studio を使用して ClickOnce アプリケーションの自動起動を無効にして、ユーザーが [スタート] メニューからアプリケーションを起動するようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowURLActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: a337a582-e67c-409a-b52e-607cd1a8fc57
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c243b0e0565c082e05fd15a1e02aa0507120e16b
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94350011"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer"></a>方法: デザイナーを使用して ClickOnce アプリケーションの URL アクティベーションを無効にする
通常、アプリケーションは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] Web サーバーからインストールされた直後に自動的に起動します。 セキュリティ上の理由から、この動作を無効にし、代わりに [ **スタート** ] メニューからアプリケーションを起動するようにユーザーに指示することができます。 次の手順では、URL アクティベーションを無効にする方法を説明します。

 この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションにのみ使用できます。 オンライン専用アプリケーションでは使用できません。このアプリケーションは、URL を使用してのみ開始できます。 オンラインのみのアプリケーションとインストールされているアプリケーションの違いの詳細については、「 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

 この手順では [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、を使用します。 このタスクは、を使用して実行することもでき [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] ます。 詳細については、「 [方法: ClickOnce アプリケーションの URL アクティベーションを無効](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)にする」を参照してください。

## <a name="procedure"></a>手順

#### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには

1. **ソリューションエクスプローラー** でプロジェクト名を右クリックし、[ **プロパティ** ] をクリックします。

2. [ **プロパティ** ] ページで、[ **発行** ] タブをクリックします。

3. **[オプション]** をクリックします。

4. [ **マニフェスト** ] をクリックします。

5. [ **ブロックアプリケーションが URL 経由でアクティブ化され** ないようにする] チェックボックスをオンにします。

6. アプリケーションをデプロイします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)