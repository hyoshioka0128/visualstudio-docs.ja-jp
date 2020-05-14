---
title: '[発行] ページ (プロジェクト デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.PropertyPage
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Project Designer, Publish page
- Publish page in Project Designer
ms.assetid: 153527c6-8b95-4003-8e8e-03a489d0a629
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 391e6c457dd09afa154c46cbc8644f028052cb32
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665705"
---
# <a name="publish-page-project-designer"></a>[発行] ページ (プロジェクト デザイナー)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー** の **[発行]** ページは、ClickOnce 配置用のプロパティを構成する場合に使用します。

 この **[発行]** ページにアクセスするには、 **ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー** が表示されたら、 **[発行]** タブをクリックします。

> [!NOTE]
> ここで説明するいくつかの ClickOnce プロパティは、 **[ビルド]** メニューの **[発行ウィザード]** または、このページの **[発行ウィザード]** ボタンをクリックして設定することも可能です。

## <a name="uielement-list"></a>UIElement の一覧
 **発行フォルダーの場所**アプリケーションが発行される場所を指定します。 ドライブ パス (`C:\deploy\myapplication`)、ファイル共有 (`\\server\myapplication`)、FTP サーバー (`ftp://ftp.microsoft.com/myapplication`)、または Web サイト (`http://www.microsoft.com/myapplication`) にすることができます。 **[発行場所]** ボックスでは、テキストは参照 ( **[...]** ) ボタンが機能する順番で並んでいる必要があります。

 既定の発行場所は、IIS をインストールしている場合は `http://localhost/<projectname>/` で、IIS をインストールしていない場合は、 `publish\` ディレクトリです。 コンピューターが Windows Vista を実行している場合、IIS がインストールされているかどうかにかかわらず、既定は常に `publish\` です。

 **インストールフォルダーの URL**Optional. ユーザーがアプリケーションをインストールする Web サイトを指定します。 これは、アプリケーションがステージング サーバーに発行されるなど、 **発行場所**と異なる場合のみ必要です。

 **インストールモードと設定**アプリケーションが**発行場所**から直接実行されるかどうかを判断します ( **[アプリケーションがオンラインでのみ利用可能な場合のみ**] が選択されているか、 **[スタート]** メニューおよび **[プログラムの追加と削除]** 項目に追加されている場合)。**コントロールパネル**( **[アプリケーションがオフラインでも利用可能な**場合] も選択されています)。

 WPF Web ブラウザー アプリケーションなどのようなアプリケーションは、オンラインでのみ利用できるため、 **[アプリケーションはオフラインでも利用できる]** は無効です。

 **アプリケーションファイル**[[アプリケーションファイル] ダイアログボックス](https://msdn.microsoft.com/b06dff3a-b87a-4caf-996b-7a4acf8137a8)を開きます。このダイアログボックスでは、個々のファイルをどのようにインストールするかを指定します。

 **前提条件**[[必須コンポーネント] ダイアログボックス](../../ide/reference/prerequisites-dialog-box.md)を開きます。このダイアログボックスは、アプリケーションと共にインストールされる前提条件コンポーネント (.NET Framework など) を指定するために使用されます。

 **更新プログラム**[[アプリケーションの更新] ダイアログボックス](https://msdn.microsoft.com/8eca8743-8e68-4d04-bfd5-4dc0a9b2934f)を開きます。このダイアログボックスは、アプリケーションの更新プログラムの動作を指定するために使用されます。 **[アプリケーションはオンラインでのみ利用できる]** が選択されている場合は、使用できません。

 **オプション**[[発行オプション] ダイアログボックス](https://msdn.microsoft.com/fd9baa1b-7311-4f9e-8ffb-ae50cf110592)を開きます。このダイアログボックスは、追加の高度な発行オプションを指定するために使用されます。

 **バージョンの発行**アプリケーションの発行バージョン番号を設定します。バージョン番号を変更すると、アプリケーションが更新プログラムとして発行されます。 **メジャー**、 **マイナー**、 **ビルド**、 **リビジョン**のバージョンの発行のそれぞれの最大値は、<xref:System.UInt16.MaxValue>で許可されている 65355 ( <xref:System.Version>) です。

 ClickOnce を使用してアプリケーションの複数のバージョンをインストールすると、以前のバージョンのアプリケーションは、指定した発行場所の Archive というフォルダーに移されます。 以前のバージョンがこのようにアーカイブされることで、インストール ディレクトリが以前のバージョンのフォルダーから分離されます。

 **発行ごとにリビジョンを自動的にインクリメント**するOptional. このオプションが選択されている場合 (既定)、バージョンの発行番号の **[リビジョン]** 部分は、アプリケーションが発行されるたびに 1 ずつインクリメントされます。 これにより、そのアプリケーションが更新プログラムとして発行されます。

 **発行ウィザード**[発行ウィザード](https://msdn.microsoft.com/fc6abebd-13d6-48e4-a567-fbc52dad0872)を開きます。 発行ウィザードの完了は、 **[ビルド]** メニューで **[発行]** コマンドを実行するのと同じ効果があります。

 **今すぐ発行**現在の設定を使用してアプリケーションを発行します。 **[発行ウィザード]** の **[完了]** ボタンと同じです。

## <a name="see-also"></a>参照
 [Clickonce アプリケーションの発行](../../deployment/publishing-clickonce-applications.md)[方法: 発行ウィザードを使用して Clickonce アプリケーションを発行](../../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する方法[: Visual Studio がファイルをコピーする場所を指定](../../deployment/how-to-specify-where-visual-studio-copies-the-files.md)する方法[: エンドユーザーがインストールする場所を指定](../../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)[する方法テクニカルサポートへのリンクを指定](../../deployment/how-to-specify-a-link-for-technical-support.md)する[方法: Clickonce のオフラインまたはオンラインインストールモードを指定](../../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)する方法[: CD インストールの自動開始を有効](../../deployment/how-to-enable-autostart-for-cd-installations.md)にする方法: [ClickOnce の発行バージョンを設定](../../deployment/how-to-set-the-clickonce-publish-version.md)する[方法: 自動的にインクリメントするClickOnce 発行バージョン](../../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)[方法: clickonce によって発行されるファイルを指定](../../deployment/how-to-specify-which-files-are-published-by-clickonce.md)する方法: clickonce[アプリケーションを使用して必須コンポーネントをインストール](../../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)する方法: [Clickonce アプリケーションの更新プログラムを管理](../../deployment/how-to-manage-updates-for-a-clickonce-application.md)する[方法: を変更するClickOnce アプリケーションの発行言語](../../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)[方法: clickonce アプリケーションのスタートメニュー名を指定](../../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)する[方法: Clickonce アプリケーションの発行ページを指定する Clickonce の](../../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)[セキュリティと配置](../../deployment/clickonce-security-and-deployment.md)
