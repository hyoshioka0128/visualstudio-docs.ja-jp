---
title: ユーザーのアクセス許可 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, user permissions
- user permissions
- administrative privileges
- permissions
ms.assetid: 70485ed7-6342-41bf-8250-7a6826e21b98
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dc49a628cdf5695df7744295d2c1d990986bcfbe
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295638"
---
# <a name="user-permissions-and-visual-studio"></a>ユーザー アクセス許可と Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

セキュリティ上の理由により、Visual Studio はできる限り通常のユーザーとして実行してください。

> [!WARNING]
> また、信頼できる人または信頼できる場所以外から入手した Visual Studio ソリューションをコンパイル、起動、またはデバッグしないでください。

 通常のユーザーでも Visual Studio IDE のほぼすべてのタスクを実行できますが、次のタスクを実行するには管理者のアクセス許可が必要です。

|区分|タスク|詳細情報|
|----------|----------|--------------------------|
|インストール|Visual Studio をインストールする。|[Visual Studio 2015 のインストール](../install/install-visual-studio-2015.md)|
||Visual Studio の評価版からアップグレードする。|[方法: 評価版の Visual Studio からアップグレードする](../install/how-to-upgrade-from-a-trial-edition-of-visual-studio.md)|
||ローカル ヘルプ コンテンツをインストール、更新、または削除する。|[ローカル コンテンツのインストールと管理](../ide/install-and-manage-local-content.md)|
|アプリケーションの種類|SharePoint 2010 のソリューションを開発する。|[SharePoint ソリューションの開発要件](https://msdn.microsoft.com/library/ae8ff69d-4540-4380-ab0b-845f7108e89c)|
||[!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)] の開発者ライセンスを取得する。|[開発者用ライセンスの取得](https://go.microsoft.com/fwlink/?LinkID=241313)|
|ツールボックス|**ツールボックス**にクラシック COM コントロールを追加する。|[ツールボックスの使用](../ide/using-the-toolbox.md)|
|アドイン|IDE でクラシック COM を使用して記述されたアドインをインストールおよび使用する。|[アドインおよびウィザードの作成](https://msdn.microsoft.com/library/c5a47c21-6668-4de3-898d-afa969317e73)|
|ビルド|コンポーネントを登録するビルド後のイベントを使用する。|[カスタム ビルド ステップとビルド イベントについて](https://msdn.microsoft.com/library/beb2f017-3e9f-4b2c-9b57-2572fd2628e4)|
||C++ プロジェクトのビルド時に登録手順を含める。|[カスタム ビルド ステップとビルド イベントについて](https://msdn.microsoft.com/library/beb2f017-3e9f-4b2c-9b57-2572fd2628e4)|
|デバッグ|昇格されたアクセス許可で実行されたアプリケーションをデバッグする。|[デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)|
||ASP.NET Web サイトなど、別のユーザー アカウントで実行されたアプリケーションをデバッグする。|[ASP.NET アプリケーションおよび AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)|
||XAML ブラウザー アプリケーション (XBAP) をゾーンでデバッグする。|[WPF ホスト (PresentationHost.exe)](https://msdn.microsoft.com/library/3215bfa1-722c-4ac8-a7c5-bdd02d30afbd)|
||エミュレーターを使用して、Microsoft Azure クラウド サービス プロジェクトをデバッグする。|[Visual Studio でのクラウド サービスのデバッグ](https://go.microsoft.com/fwlink/?LinkId=266725)|
||リモート デバッグのファイアウォールを構成する。|[デバイスのリモート ツールのセットアップ](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)|
|パフォーマンス ツール|アプリケーションをプロファイルする。|[パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-performance-profiling.md)|
|配置|ローカル コンピューターでインターネット インフォメーション サービス (IIS) に Web アプリケーションを配置する。|[Visual Studio または Visual Web Developer を使用しているホスティング プロバイダーへの ASP.NET Web アプリケーションの配置: テスト環境としての IIS への配置](https://go.microsoft.com/fwlink/?LinkId=266478)|
|Microsoft にフィードバックを提供する。|Visual Studio カスタマー エクスペリエンス向上プログラムへの参加方法を変更する。|[方法: フィードバックを送信する](../misc/how-to-send-feedback-about-visual-studio.md)|

## <a name="running-visual-studio-as-an-administrator"></a>管理者としての Visual Studio の実行
 IDE を起動するたびに管理アクセス許可を使用して Visual Studio を起動するか、管理アクセス許可で常に実行するようにアプリケーション ショートカットを変更できます。 詳細については、Windows のヘルプを参照してください。

#### <a name="to-run-visual-studio-with-administrative-permissions-on-includewin8includeswin8-mdmd-includewin81includeswin81-mdmd-includewinserver8includeswinserver8-mdmd-or-includewinblue_server_2includeswinblue-server-2-mdmd"></a>[!INCLUDE[win8](../includes/win8-md.md)]、[!INCLUDE[win81](../includes/win81-md.md)]、[!INCLUDE[winserver8](../includes/winserver8-md.md)]、または [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)] で管理アクセス許可を使用して Visual Studio を実行するには

1. **[スタート]** 画面で、「**Visual Studio**」と入力します。 インストールされている Visual Studio のバージョンが表示されます。

2. 起動する Visual Studio のバージョンを選択し、ショートカット メニューを表示します (画面の下部に表示されます)。 **[管理者として実行]** を選択します。

     Visual Studio の起動時には、 **[(管理者)]** がタイトル バーの製品名の後に表示されます。

#### <a name="to-run-visual-studio-with-administrative-permissions-on-includewin7includeswin7-mdmd-or-includewinsvr08_r2includeswinsvr08-r2-mdmd"></a>または [!INCLUDE[win7](../includes/win7-md.md)] で管理アクセス許可を使用して Visual Studio を実行するには[!INCLUDE[winsvr08_r2](../includes/winsvr08-r2-md.md)]

1. **[スタート]** メニューをクリックし、 **[すべてのプログラム]** をクリックします。

2. **[Microsoft Visual Studio** *Version]* フォルダーで、 **[Visual Studio** *Version]* をクリックし、ショートカット メニューを開き、 **[管理者として実行]** をクリックします。

     Visual Studio の起動時には、 **[(管理者)]** がタイトル バーの製品名の後に表示されます。

## <a name="see-also"></a>関連項目
 [Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/porting-migrating-and-upgrading-visual-studio-projects.md) [Visual Studio 2015 のインストール](../install/install-visual-studio-2015.md)
