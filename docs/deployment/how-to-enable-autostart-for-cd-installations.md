---
title: CD インストールの自動開始を有効にする |Microsoft Docs
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28fa4830c3ea5ff840e0d58f6d31f718c28ec3fb
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90850944"
---
# <a name="how-to-enable-autostart-for-cd-installations"></a>方法: CD インストールの自動開始を有効にする
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]Cd-rom や dvd-rom などのリムーバブルメディアを使用してアプリケーションを展開する場合は、 `AutoStart` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] メディアが挿入されたときにアプリケーションが自動的に起動するように、を有効にすることができます。

 `AutoStart`は、**プロジェクトデザイナー**の [**発行**] ページで有効にすることができます。

### <a name="to-enable-autostart"></a>自動開始を有効にするには

1. **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。

2. **[公開]** タブをクリックします。

3. **[オプション]** ボタンをクリックします。

     [ **発行オプション** ] ダイアログボックスが表示されます。

4. **[デプロイ]** をクリックします。

5. [Cd **インストールの場合、cd の挿入時にセットアップを自動的に開始する** ] チェックボックスをオンにします。

     アプリケーションが発行されると、自動実行の *.inf* ファイルが発行場所にコピーされます。

## <a name="see-also"></a>こちらもご覧ください
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)