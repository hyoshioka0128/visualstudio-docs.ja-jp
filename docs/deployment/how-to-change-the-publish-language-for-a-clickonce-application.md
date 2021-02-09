---
title: ClickOnce アプリケーションの発行言語を変更する
description: 開発用コンピューターの言語またはカルチャを既定として使用するのではなく、ClickOnce でローカライズアプリケーションの言語/カルチャを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish language property
- ClickOnce deployment, changing publish language
- publishing, ClickOnce
ms.assetid: ef5024c4-cda1-4970-bc75-32a2a10c92c3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c0d9c3d49dde0bdef41e89ee71139fb1ab621297
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851466"
---
# <a name="how-to-change-the-publish-language-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションに使用する発行の言語を変更する

アプリケーションを公開する場合 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、インストール時に表示されるユーザーインターフェイスは、既定で開発用コンピューターの言語とカルチャになります。 ローカライズされたアプリケーションを発行する場合、ローカライズされたバージョンと一致する言語とカルチャを指定する必要があります。 これは、プロジェクトのプロパティによって決定され `Publish language` ます。

`Publish language`プロパティは、**プロジェクトデザイナー** の [**発行**] ページからアクセスできる [**発行オプション**] ダイアログボックスで設定できます。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="to-change-the-publish-language"></a>発行言語を変更するには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. [ **オプション** ] ボタンをクリックして、[ **発行オプション** ] ダイアログボックスを開きます。

4. [ **説明**] をクリックします。

5. [ **発行オプション** ] ダイアログボックスで、[ **発行言語** ] ドロップダウンリストから言語とカルチャを選択し、[ **OK**] をクリックします。

## <a name="see-also"></a>関連項目

- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)