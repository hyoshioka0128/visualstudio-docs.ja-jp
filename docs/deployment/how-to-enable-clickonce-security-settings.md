---
title: '方法: ClickOnce のセキュリティ設定を有効にする |Microsoft Docs'
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d673edac957e9625f7d948fbe766ee08b23b6b52
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382433"
---
# <a name="how-to-enable-clickonce-security-settings"></a>方法: ClickOnce のセキュリティ設定を有効にする
アプリケーションを発行するには、ClickOnce アプリケーションのコードアクセスセキュリティを有効にする必要があります。 これは、発行ウィザードを使用してアプリケーションを発行するときに自動的に実行されます。

 場合によっては、アプリケーションをビルドまたはデバッグするときに、コードアクセスセキュリティを有効にするとパフォーマンスが低下することがあります。このような場合は、セキュリティ設定を一時的に無効にすることをお勧めします。

 ClickOnce のセキュリティ設定は、**プロジェクトデザイナー**の [**セキュリティ**] ページで有効または無効にすることができます。

### <a name="to-enable-clickonce-security-settings"></a>ClickOnce セキュリティ設定を有効にするには

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[セキュリティ]** タブをクリックします。

3. **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにします。

     [セキュリティ] ページで、アプリケーションのセキュリティ設定をカスタマイズできるようになりました。

    > [!NOTE]
    > このチェックボックスは、**発行**ウィザードを使用してアプリケーションを発行するたびに自動的に選択されます。

### <a name="to-disable-clickonce-security-settings"></a>ClickOnce のセキュリティ設定を無効にするには

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[セキュリティ]** タブをクリックします。

3. [ **ClickOnce セキュリティ設定を有効にする**] チェックボックスをオフにします。

     アプリケーションは、完全な信頼セキュリティ設定を使用して実行されます。[**セキュリティ**] ページの設定はすべて無視されます。

    > [!NOTE]
    > アプリケーションが発行ウィザードを使用して発行されるたびに、このチェックボックスがオンになります。発行が成功するたびに、もう一度オフにする必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
