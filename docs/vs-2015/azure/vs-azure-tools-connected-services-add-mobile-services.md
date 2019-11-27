---
title: 接続済みサービスを使用した Mobile Services の追加
description: Visual Studio の [接続済みサービスの追加] ダイアログボックスを使用して Mobile Services を追加する
documentationcenter: na
author: ghogen
manager: jillfra
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.topic: conceptual
ms.workload: azure-vs
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: 4f84970daea03904d4642317cf6097beb07be7f1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300180"
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Visual Studio を使用した Mobile Services の追加接続済みサービス
Visual Studio 2015 では、 **[接続済みサービスの追加]** ダイアログボックスを使用して Azure Mobile Services に接続できます。 任意C#のクライアントアプリ、任意の JavaScript アプリ、またはクロスプラットフォーム Cordova アプリから接続できます。 接続すると、データを作成してアクセスしたり、カスタム Api やスケジュールされたジョブを作成したり、プッシュ通知のサポートを追加したりすることができます。  接続済みサービス操作は、すべての適切な参照と接続コードを追加します。 また、Azure AD、Facebook、Twitter、Microsoft アカウントなど、さまざまな一般的な id スキームを使用して、認証の組み込みサポートを利用することもできます。

## <a name="supported-project-types"></a>サポートされているプロジェクトの種類
> [!NOTE]
> Visual Studio 2015 では、[接続済みサービスの追加] ダイアログを使用した Windows ユニバーサル (Windows 10) プロジェクトへの Azure Mobile Services の追加はサポートされていません。 プロジェクトの NuGet パッケージマネージャーを使用して適切なパッケージをインストールすることによって、Azure Mobile Services を追加できます。
>
>

[接続済みサービス] ダイアログボックスを使用して、次の種類のプロジェクトで Azure Mobile Services に接続できます。

* .NET Windows 8.1 ストア、電話、ユニバーサルアプリプロジェクト
* JavaScript Windows 8.1 ストア、電話、ユニバーサルアプリプロジェクト
* Apache Cordova の Visual Studio Tools を使用して作成されたプロジェクト

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a>[接続済みサービスの追加] ダイアログボックスを使用して Azure Mobile Services に接続する
1. Azure アカウントを持っていることを確認します。 Azure アカウントを持っていない場合は、[無料試用版](https://go.microsoft.com/fwlink/?LinkId=518146)にサインアップできます。
2. **[接続済みサービスの追加]** ダイアログボックスを開きます。

   * .NET アプリの場合は、Visual Studio でプロジェクトを開き、ソリューションエクスプローラーの **[参照]** ノードのコンテキストメニューを開き、 **[接続済みサービスの追加]** を選択します。

        ![Azure モバイルサービスに接続しています](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Apache Cordova アプリプロジェクトの場合は、Visual Studio でプロジェクトを開き、ソリューションエクスプローラーでプロジェクトノードのコンテキストメニューを開き、 **[接続済みサービスの追加]** を選択します。
3. **[接続済みサービスの追加]** ダイアログ ボックスで、 **[Azure Mobile Services]** を選択し、 **[構成]** をクリックします。 Azure にまだログインしていない場合は、ログインするように求められる場合があります。

    ![Azure モバイルサービスを追加する](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. **[Azure Mobile Services]** ダイアログ ボックスで、既存のモバイル サービスがある場合は、それを選択します。 新しい Azure mobile service を作成する必要がある場合は、以下の手順に従ってください。 それ以外の場合は次の手順に進みます。

    新しいモバイルサービスアカウントを作成するには、次のようにします。

   1. ダイアログ ボックスの下部にある **[サービスの作成]** リンクを選択します。
       新しいモバイル接続されたサービス](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png) を追加 ![には
   2. **[モバイルサービスの作成]** ダイアログボックスで、 **[ランタイム]** ドロップダウンリストから、JavaScript バックエンドモバイルサービスまたは .net バックエンドモバイルサービスを選択できます。

       ![モバイルサービスの作成](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)

       JavaScript バックエンドサービスは、単純で強力です。 JavaScript バックエンド モバイル サービスを作成する場合、サーバー側の JavaScript コードはクラウドで格納されますが、サーバー エクスプローラーまたは Azure の管理ポータルを使用することで、サーバー スクリプトを編集できます。

       .NET バックエンドモバイルサービスを使用すると、Web API と Entity Framework の能力と柔軟性を最大限に高めることができます。 .NET バックエンドモバイルサービスを作成すると、プロジェクトが作成され、ソリューションに追加されます。
   3. モバイル サービスを必要とする **[リージョン]** を選択し、サーバーのユーザー名とパスワードを入力します。
   4. 必要な情報をすべて入力したら、 **[作成]** クリックしてモバイル サービスを作成します。
   5. 新しいモバイルサービスが **[Azure Mobile Services]** ダイアログボックスのサービスの一覧に表示されます。 一覧の新しいモバイル サービスを選択し、 **[追加]** をクリックして、そのサービスをプロジェクトに追加します。
5. 表示される [作業の開始] ページを確認し、プロジェクトがどのように変更されたかを確認します。 [作業の開始] ページは、接続済みサービスを追加するたびにブラウザーに表示されます。 推奨される次の手順とコード例を確認したり、[現象] ページに切り替えて、プロジェクトに追加された参照と、コードと構成ファイルがどのように変更されたかを確認したりすることができます。
6. コードサンプルをガイドとして使用して、モバイルサービスにアクセスするコードの記述を開始します。

## <a name="how-your-project-is-modified"></a>プロジェクトを変更する方法
Visual Studio がプロジェクトを変更する方法は、プロジェクトの種類によって異なります。 クライアントC#アプリについては、「変更[点– C#プロジェクト](https://go.microsoft.com/fwlink/p/?LinkId=513119)」を参照してください。 JavaScript クライアントアプリについては、「変更[点– javascript プロジェクト](https://go.microsoft.com/fwlink/p/?LinkId=513120)」を参照してください。 Cordova アプリについては、「変更[点– cordova プロジェクト](https://go.microsoft.com/fwlink/p/?LinkId=513116)」を参照してください。

## <a name="next-steps"></a>次のステップ:
質問してヘルプを表示します。

* [MSDN フォーラム: Azure Mobile Services](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Microsoft Azure チームブログの Azure Mobile Services](https://azure.microsoft.com/blog/topics/mobile/)
* [Azure.microsoft.com での Azure の Mobile Services](https://azure.microsoft.com/services/mobile-services/)
* [Azure.microsoft.com の Azure Mobile Services ドキュメント](https://azure.microsoft.com/documentation/services/mobile-services/)
