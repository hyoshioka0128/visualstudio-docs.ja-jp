---
title: '[セキュリティの詳細設定] ダイアログ ボックス'
ms.date: 06/27/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.err.debug_in_zone_no_hostproc
helpviewer_keywords:
- Advanced Security Settings dialog box
ms.assetid: 2e7aefe9-6d20-4f3e-b257-aee1ebcc6f5d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dce482f53f9f3e6dd0b57d6cb905f97cdfaa601a
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2018
ms.locfileid: "39180517"
---
# <a name="advanced-security-settings-dialog-box"></a>[セキュリティの詳細設定] ダイアログ ボックス

このダイアログ ボックスでは、ゾーンでのデバッグに関連するセキュリティ設定を指定することができます。

![Visual Studio の [セキュリティの詳細設定] ダイアログ ボックス](../media/advanced-security-settings.png)

このダイアログ ボックスを表示するには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。 **プロジェクト デザイナー**が表示されたら、[**セキュリティ**] タブをクリックします。**[セキュリティ]** ページで **[ClickOnce セキュリティ設定を有効にする]** を選び、**[これは部分的に信頼するアプリケーションです]** をクリックして、**[詳細]** をクリックします。

## <a name="uielement-list"></a>UIElement の一覧

**[アプリケーションにその元のサイトへのアクセス権を与える]**

このチェック ボックスをオンにすると、アプリケーションは発行されている Web サイトまたはサーバー共有にアクセスできます。 既定では、このチェック ボックスはオンになっています。

**[このアプリケーションが次の URL からダウンロードされたと仮定してデバッグする]**

**[発行]** ページで指定した **[インストール URL]** に対応する Web サイトまたはサーバー共有にアプリケーションがアクセスできるようにする必要がある場合は、ここでその URL を入力します。 このオプションは、**[アプリケーションにその元のサイトへのアクセス権を与える]** が選択されている場合にのみ使用できます。

## <a name="see-also"></a>関連項目

- [[セキュリティ] ページ (プロジェクト デザイナー)](../../ide/reference/security-page-project-designer.md)