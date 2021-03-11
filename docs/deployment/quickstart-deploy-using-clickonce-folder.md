---
description: Visual Studio 2019 バージョン 16.8 以降では、 [発行] ツールを使用し、Visual Studio から ClickOnce を使って .NET Core 3.1、またはそれ以降の Windows デスクトップ アプリケーションを発行することができます。
title: ClickOnce を使用して .NET Windows デスクトップ アプリケーションを配置する
ms.date: 10/15/2020
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder, ClickOnce
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: john-hart
ms.author: JohnHart
manager: jmartens
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: d3977408f191aabc734226fd6b637fcfaaf5e9de
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165710"
---
# <a name="deploy-a-net-windows-desktop-application-using-clickonce"></a>ClickOnce を使用して .NET Windows デスクトップ アプリケーションを配置する

Visual Studio 2019 バージョン 16.8 以降では、 **[発行]** ツールを使用し、Visual Studio から ClickOnce を使って .NET Core 3.1、またはそれ以降の Windows デスクトップ アプリケーションを発行することができます。

> [!NOTE]
> .NET Framework Windows アプリケーションを発行する必要がある場合は、[ClickOnce を使用したデスクトップ アプリの配置](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) (C# または Visual Basic) に関するページを参照してください。

## <a name="publishing-with-clickonce"></a>ClickOnce を使用した発行

1. ソリューション エクスプローラーで、プロジェクトを右クリックして、 **[発行]** を選択します (または **[ビルド]**  >  **[発行]** メニュー項目を使用します)。

    ![ソリューション エクスプローラーのプロジェクト コンテキスト メニューにある [発行] コマンド](../deployment/media/quickstart-clickonce-solution-explorer.png "[発行] を選択する")

1. 以前に発行プロファイルを構成した場合は、 **[発行]** ページが表示されます。 **[新規]** を選択します。

1. **[発行]** ウィザードで、 **[フォルダー]** を選択します。

    ![発行先としてフォルダーを選択する](../deployment/media/quickstart-clickonce-publish-folder-category.png "フォルダーの選択")

1. **[特定のターゲット]** ページで、 **[ClickOnce]** を選択します。

    ![特定のターゲットとして [ClickOnce] を選択する](../deployment/media/quickstart-clickonce-publish-folder-target.png "ClickOnce を選択する")

1. パスを入力するか、 **[参照]** を選択して発行場所を選びます。

    ![発行場所のパスを指定する](../deployment/media/quickstart-clickonce-publish-location.png "パスを入力する")

1. **[インストール場所]** ページで、ユーザーがアプリケーションをインストールする場所を選択します。

    ![フォルダーのパスを指定する](../deployment/media/quickstart-clickonce-install-location.png "インストール場所を選択する")

1. **[設定]** ページで、ClickOnce に必要な設定を指定できます。

1. UNC パスまたは Web サイトからインストールすることを選択した場合は、このページでアプリケーションをオフラインで使用できるようにするかどうかを指定できます。 このオプションをオンにすると、ユーザーの [スタート] メニューにアプリケーションが一覧表示され、新しいバージョンが発行されたときにアプリケーションを自動的に更新できるようになります。 既定では、更新プログラムはインストール場所から入手できます。  更新プログラムに別の場所を使用したい場合は、[設定の更新] リンクを使用して、そのように指定できます。 アプリケーションをオフラインで使用できるようにしない場合は、インストール場所から実行されます。

    ![発行設定を指定する](../deployment/media/quickstart-clickonce-unc-settings.png "発行設定を選択する")

1. CD、DVD または USB ドライブからインストールすることを選択した場合は、このページで、アプリケーションで自動更新をサポートするかどうかを指定することもできます。 更新プログラムをサポートすることを選択した場合は、場所の更新は必須であり、有効な UNC パスまたは Web サイトである必要があります。

    ![発行設定を選択する](../deployment/media/quickstart-clickonce-settings.png "発行設定を選択する")

このページには、セットアップに含める **アプリケーション ファイル**、インストールする **前提条件** のパッケージ、およびその他の **オプション** を、ページの上部にあるリンクを使用して指定する機能が含まれています。

また、このページでは、発行バージョンと、発行のたびにバージョンが自動的に増分されるようにするかどうかを設定できます。

> [!NOTE]
> 発行バージョン番号は、各 ClickOnce プロファイルに対して一意となります。 複数のプロファイルを使用する予定の場合は、この点に注意する必要があります。

10. **[マニフェストの署名]** ページで、マニフェストに署名するかどうかと、使用する証明書を指定できます。

    ![ClickOnce マニフェストに署名する](../deployment/media/quickstart-clickonce-sign-manifests.png)

1. **[構成]** ページで、必要なプロジェクト構成を選択できます。

     ![発行構成を指定する](../deployment/media/quickstart-clickonce-configuration.png)

    選択する設定の詳細については、以下を参照してください。

    - [フレームワーク依存と自己完結型の展開](/dotnet/core/deploying/)
    - [ターゲット ランタイム識別子 (ポータブル RID など)](/dotnet/core/rid-catalog)
    - [デバッグ構成とリリース構成](../ide/understanding-build-configurations.md)

1. **[完了]** を選択して新しい ClickOnce 発行プロファイルを保存します。

1. **[概要]** ページで、 **[発行]** を選択すると、Visual Studio によりプロジェクトがビルドされ、指定された発行フォルダーに発行されます。 このページにはプロファイルの概要も表示されます。

    ![プロファイルの概要を示す [発行] プロパティ ウィンドウ](../deployment/media/quickstart-clickonce-summary.png)

1. 再発行するには、 **[発行]** を選択します。

## <a name="next-steps"></a>次の手順

.NET アプリの場合:

- [.NET Framework およびアプリケーションの配置](/dotnet/framework/deployment/)
- [ClickOnce に関するリファレンス](clickonce-reference.md)
