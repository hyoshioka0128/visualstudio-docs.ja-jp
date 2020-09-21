---
title: エンドユーザーのインストール元の場所を指定します
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ba02b1cf8947fa2d1907d6316e36af8f8f54a77
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808725"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>方法: エンド ユーザーがインストールを開始する場所を指定する

アプリケーションを発行するときに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、ユーザーがアプリケーションをダウンロードしてインストールする場所は、必ずしもアプリケーションを最初に発行する場所とは限りません。 たとえば、一部の組織では、開発者がアプリケーションをステージングサーバーに発行した後、管理者がアプリケーションを Web サーバーに移動する場合があります。

この場合、プロパティを使用して、 `Installation URL` ユーザーがアプリケーションをダウンロードする Web サーバーを指定できます。 これは、アプリケーションマニフェストが更新プログラムを検索する場所を認識できるようにするために必要です。

プロパティは、 `Installation URL` **プロジェクトデザイナー**の [**発行**] ページで設定できます。

> [!NOTE]
> プロパティは、 `Installation URL` **publishwizard**を使用して設定することもできます。 詳細については、「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。

### <a name="to-specify-an-installation-url"></a>インストール URL を指定するには

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. [インストール URL] フィールドに、形式を使用した完全修飾 URL `https://www.contoso.com/ApplicationName` または形式の UNC パスを使用して、インストール先を入力し `\Server\ApplicationName` ます。

## <a name="see-also"></a>こちらもご覧ください
- [方法: Visual Studio がファイルをコピーする場所を指定する](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)