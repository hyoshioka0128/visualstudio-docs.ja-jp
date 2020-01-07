---
title: '[セキュリティの詳細設定] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.err.debug_in_zone_no_hostproc
- vs.err.debug_in_zone_no_hostproc:11310
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Advanced Security Settings dialog box
ms.assetid: 2e7aefe9-6d20-4f3e-b257-aee1ebcc6f5d
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 000c3c4e2996869e96fd0d6097b5bab8576936a7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651736"
---
# <a name="advanced-security-settings-dialog-box"></a>[セキュリティの詳細設定] ダイアログ ボックス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このダイアログ ボックスでは、ゾーンでのデバッグに関連するセキュリティ設定を指定することができます。

 このダイアログ ボックスを表示するには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されたら、 **[セキュリティ]** タブをクリックします。**セキュリティ]** [ ページで ]**ClickOnce セキュリティ設定を有効にする**[ を選び、]**これは部分的に信頼するアプリケーションです**[ をクリックして、] **[詳細** をクリックします。

## <a name="uielement-list"></a>UIElement の一覧
 **選択されたアクセス許可セットでこのアプリケーションをデバッグする** このチェック ボックスをオンにすると、 **[セキュリティ]** ページで選択されたアクセス許可セットがデバッグ中に使われます。 既定では、このチェック ボックスはオンになっています。

 セキュリティ ゾーンでのデバッグが動作するためには、このオプションを有効にする必要があります。また、 **[Visual Studio ホスティング プロセスを有効にする]** オプション (**プロジェクト デザイナー**の **[デバッグ]** ページで利用可能) も有効にする必要があります。

 WPF Web ブラウザー アプリケーション プロジェクトの場合、 **[選択されたアクセス許可セットでこのアプリケーションをデバッグする]** オプションはオンに設定され、変更できなくなっています。

 **アプリケーションにその元のサイトへのアクセス権を与える** このチェック ボックスをオンにすると、アプリケーションは発行されている Web サイトまたはサーバー共有にアクセスできます。 既定では、このチェック ボックスはオンになっています。

 **このアプリケーションが次の URL からダウンロードされたと仮定してデバッグする** **[発行]** ページで指定した **[インストール URL]** に対応する Web サイトまたはサーバー共有にアプリケーションがアクセスできるようにする必要がある場合は、ここでその URL を入力します。 このオプションは、 **[アプリケーションにその元のサイトへのアクセス権を与える]** が選択されている場合にのみ使用できます。

## <a name="see-also"></a>関連項目
 [[セキュリティ] ページ (プロジェクト デザイナー)](../../ide/reference/security-page-project-designer.md)
