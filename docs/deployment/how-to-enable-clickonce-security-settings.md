---
title: ClickOnce セキュリティ設定を有効にする |Microsoft Docs
description: 発行ウィザードが ClickOnce アプリケーションのコードアクセスセキュリティを自動的に有効にしてアプリケーションを公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- security [Visual Studio], ClickOnce applications
- ClickOnce deployment, security settings
- security settings, ClickOnce deployment
ms.assetid: 73cd3e9d-cd72-4ad2-8cae-94d6bb6b01e0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 758aecc4f2bf280fd7ff5ca7ca482ee6a3e3d68d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900649"
---
# <a name="how-to-enable-clickonce-security-settings"></a>方法: ClickOnce のセキュリティ設定を有効にする
アプリケーションを発行するには、ClickOnce アプリケーションのコードアクセスセキュリティを有効にする必要があります。 これは、発行ウィザードを使用してアプリケーションを発行するときに自動的に実行されます。

 場合によっては、アプリケーションをビルドまたはデバッグするときに、コードアクセスセキュリティを有効にするとパフォーマンスが低下することがあります。このような場合は、セキュリティ設定を一時的に無効にすることをお勧めします。

 ClickOnce のセキュリティ設定は、**プロジェクトデザイナー** の [**セキュリティ**] ページで有効または無効にすることができます。

### <a name="to-enable-clickonce-security-settings"></a>ClickOnce セキュリティ設定を有効にするには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[セキュリティ]** タブをクリックします。

3. **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにします。

     [セキュリティ] ページで、アプリケーションのセキュリティ設定をカスタマイズできるようになりました。

    > [!NOTE]
    > このチェックボックスは、 **発行** ウィザードを使用してアプリケーションを発行するたびに自動的に選択されます。

### <a name="to-disable-clickonce-security-settings"></a>ClickOnce のセキュリティ設定を無効にするには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[セキュリティ]** タブをクリックします。

3. [ **ClickOnce セキュリティ設定を有効にする** ] チェックボックスをオフにします。

     アプリケーションは、完全な信頼セキュリティ設定を使用して実行されます。[ **セキュリティ** ] ページの設定はすべて無視されます。

    > [!NOTE]
    > アプリケーションが発行ウィザードを使用して発行されるたびに、このチェックボックスがオンになります。発行が成功するたびに、もう一度オフにする必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
