---
title: ClickOnce 発行バージョンの自動インクリメント
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f6267e75db2e2a23d01368cdaa822d835cb8b844
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809795"
---
# <a name="how-to-automatically-increment-the-clickonce-publish-version"></a>方法: ClickOnce の発行するバージョンを自動的にインクリメントする

アプリケーションを公開するときに、プロパティを変更すると、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version` アプリケーションが更新プログラムとして発行されます。 既定では、アプリケーションを発行するたびに、Visual Studio によっての数が自動的に増加し `Revision` `Publish Version` ます。

この動作は、**プロジェクトデザイナー**の [**発行**] ページで無効にすることができます。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="to-disable-automatically-incrementing-the-publish-version"></a>発行バージョンを自動的にインクリメントしないようにするには

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. [ **発行バージョン** ] セクションで、[ **リリースごとにリビジョンを自動的にインクリメント** する] チェックボックスをオフにします。

## <a name="see-also"></a>こちらもご覧ください

- [方法: ClickOnce の発行バージョンを設定する](../deployment/how-to-set-the-clickonce-publish-version.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)