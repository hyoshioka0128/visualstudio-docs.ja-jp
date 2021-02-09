---
title: CD インストールの自動開始を有効にする |Microsoft Docs
description: CD-ROM や DVD-ROM などのリムーバブルメディアを使用して ClickOnce アプリケーションを展開するときに自動開始を有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, AutoStart
- ClickOnce deployment, installation on CD or DVD
- deploying applications [ClickOnce], installation on CD or DVD
ms.assetid: caaec619-900c-4790-90e3-8c91f5347635
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b157df8666223e72a1e36d58505a5c087b0351bf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900688"
---
# <a name="how-to-enable-autostart-for-cd-installations"></a>方法: CD インストールの自動開始を有効にする
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]Cd-rom や dvd-rom などのリムーバブルメディアを使用してアプリケーションを展開する場合は、 `AutoStart` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] メディアが挿入されたときにアプリケーションが自動的に起動するように、を有効にすることができます。

 `AutoStart`は、**プロジェクトデザイナー** の [**発行**] ページで有効にすることができます。

### <a name="to-enable-autostart"></a>自動開始を有効にするには

1. **ソリューションエクスプローラー** でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。

2. **[公開]** タブをクリックします。

3. **[オプション]** ボタンをクリックします。

     [ **発行オプション** ] ダイアログボックスが表示されます。

4. **[デプロイ]** をクリックします。

5. [Cd **インストールの場合、cd の挿入時にセットアップを自動的に開始する** ] チェックボックスをオンにします。

     アプリケーションが発行されると、自動実行の *.inf* ファイルが発行場所にコピーされます。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)