---
title: ClickOnce の発行バージョンを設定する |Microsoft Docs
description: アプリケーションが更新プログラムであるかどうかを判断する ClickOnce 発行バージョンプロパティを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, setting publish version
- publishing, ClickOnce
- Publish Version property
ms.assetid: 06f15504-6385-40a6-b01d-cd90ca36dc73
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 100c3cd12a3011d35445ac885333802e28b4a92f
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94349790"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>方法: ClickOnce の発行バージョンを設定する
プロパティは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version` 発行するアプリケーションが更新プログラムとして扱われるかどうかを決定します。 バージョンがインクリメントされるたびに、アプリケーションが更新プログラムとして発行されます。

 プロパティは、 `Publish Version` **プロジェクトデザイナー** の [ **発行** ] ページで設定できます。

> [!NOTE]
> アプリケーションが発行されるたびにプロパティが自動的にインクリメントされるプロジェクトオプションがあります。 `Publish Version` このオプションは既定で有効になっています。 詳細については、「 [方法: ClickOnce の発行バージョンを自動的にインクリメント](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)する」を参照してください。

### <a name="to-change-the-publish-version"></a>発行バージョンを変更するには

1. **ソリューションエクスプローラー** でプロジェクトを選択し、[ **プロジェクト** ] メニューの [ **プロパティ** ] をクリックします。

2. **[公開]** タブをクリックします。

3. [ **バージョンの発行** ] フィールドで、 **メジャー** 、 **マイナー** 、 **ビルド** 、 **リビジョン** の各バージョン番号を増分します。

    > [!NOTE]
    > バージョン番号を減らすことはできません。これを行うと、予測できない更新動作が発生する可能性があります。

## <a name="see-also"></a>関連項目
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [方法: ClickOnce の発行バージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)