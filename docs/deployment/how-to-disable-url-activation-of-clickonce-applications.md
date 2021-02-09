---
title: ClickOnce アプリの URL アクティベーションを無効にする
description: ユーザーが [スタート] メニューからアプリケーションを起動できるようにする場合に、ClickOnce アプリケーションのインストール時に自動開始を無効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowUrlActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: db31a16b-960f-4264-91d7-c7c40f876068
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1e721199716abc47e89dc9fd2c7c510926853439
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900699"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications"></a>方法: ClickOnce アプリケーションの URL アクティべーションを無効にする

通常、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは Web サーバーからインストールされた直後に自動的に起動します。 ただし、セキュリティ上の理由から、この動作を無効にすることもできます。その場合は、**[スタート]** メニューからアプリケーションを起動するようにユーザーに通知します。 次の手順では、URL アクティベーションを無効にする方法を説明します。

この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションにのみ使用できます。 URL を使用する方法でのみ起動できるオンライン専用のアプリケーションには使用できません。 オンライン専用アプリケーションとインストールされたアプリケーションの違いの詳細については、「[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

この手順では、Windows Software Development Kit (SDK) ツール MageUI.exe を使用します。 このツールの詳細については、「 [MageUI.exe (マニフェスト生成および編集ツール、グラフィカルクライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)」を参照してください。 この手順は、Visual Studio を使用して実行することもできます。

## <a name="procedure"></a>プロシージャ

### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには

1. MageUI.exe で配置マニフェストを開きます。 まだ作成していない場合は、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の手順に従います。

2. **[配置オプション]** タブを選択します。

3. **[インストール後にアプリケーションを自動的に実行する]** チェックボックスをオフにします。

4. マニフェストを保存し、署名します。

## <a name="see-also"></a>関連項目

- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)