---
title: 接続済みサービス
description: Visual Studio for Mac からモバイル アプリに Azure データ ストレージ、認証、およびプッシュ通知を追加する
ms.assetid: 41CB62FF-0F39-4CE8-8917-6A77F058719F
author: sayedihashimi
ms.author: sayedha
ms.date: 11/06/2018
ms.topic: how-to
ms.openlocfilehash: 8a1287d82096677d20a498756de3d2a9f5af259b
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938764"
---
# <a name="connected-services-walkthrough"></a>接続済みサービスのチュートリアル

接続済みサービスのワークフローにより、Visual Studio for Mac に、Azure Portal のワークフローが組み込まれます。これにより、サービスを追加するために、プロジェクトを終了する必要がありません。

このチュートリアルでは、クロスプラットフォーム Xamarin.Forms ポータブル クラス ライブラリ (PCL) アプリケーションに、クラウド データ ストレージ、認証、およびプッシュ通知を提供する Azure バックエンド サービスを追加する方法を説明します。

1. まず、ソリューションの **[接続済みサービス]** をダブルクリックすると、 **[Services Gallery]** \(サービス ギャラリー\) が表示されます。
  この一覧は、そのアプリケーションの種類で利用可能なすべてのサービスです。 サービス (**Azure App Service を使用したモバイル バックエンド** など) をクリックして選択します。

    [![Visual Studio for Mac の接続済みサービス ノード](media/connected-services-image001-sml.png "Visual Studio for Mac の接続済みサービス ノード")](media/connected-services-image001.png#lightbox)

2. [サービスの詳細] ページには、サービスとインストールする必要のある依存関係の説明があります。
  **[追加]** をクリックして、アプリに依存関係を追加します。

    [![Azure を使用したモバイル バックエンド](media/connected-services-image002-sml.png "Azure を使用したモバイル バックエンド")](media/connected-services-image002.png#lightbox)

3. 依存関係が機能するには、PCL とプラットフォーム固有のプロジェクトの両方にそれが追加される必要があります。
  それを (直接または間接的に) 参照するすべてのプロジェクトにサービスが追加されるように、チェックボックスを選択します。

    [![サービスを参照する必要があるすべてのプロジェクトを確認する](media/connected-services-image003-sml.png "サービスを参照する必要があるすべてのプロジェクトを確認する")](media/connected-services-image003.png#lightbox)

4. NuGet パッケージの **[ライセンスの同意]** ダイアログで **[同意]** を選択します。
  MobileClient と依存関係、およびオフライン データ同期に必要な SQLiteStore 用の 2 つのダイアログ ボックスで同意する必要がある場合があります。

    [![ライセンス契約に同意する](media/connected-services-image004-sml.png "ライセンス契約に同意する")](media/connected-services-image004.png#lightbox)

    ![[ライセンスの同意] ウィンドウ](media/connected-services-image005.png "[ライセンスの同意] ウィンドウ")

5. 依存関係が追加されると、Azure との通信に使用するアカウントでログインを求められます。
  既に Microsoft ID を使用してログインしている場合、Visual Studio for Mac によって Azure サブスクリプションとそれらに関連付けられているすべてのアプリケーション サービスの取得が試行されます。 サブスクリプションがない場合、無料の試用版にサインアップするか、Azure ポータルでサブスクリプション プランを購入します。

6. 一覧からアプリのサービスを選択します。 これにより、Azure のアプリ サービスの URL に対応する `MobileServiceClient` オブジェクトのテンプレート コードが埋め込まれます。

    [![一覧からアプリ サービスを選択する](media/connected-services-image006-sml.png "一覧からアプリ サービスを選択する")](media/connected-services-image006.png#lightbox)

    一覧にサービスがない場合、 **[新規]** ボタンをクリックします (手順 9 を参照)。

7. PCL に `MobileServiceClient` のテンプレート コードをコピーします。 ファイルの場所は、それが 1 インスタンスしかない場合は重要ではありません。
  Azure のすべての対話を処理し、`MobileServiceClient`を使用する `AzureService` クラスを作成するのが推奨されるアプローチです。

    ![構成コードをアプリにコピーする](media/connected-services-image007.png "構成コードをアプリにコピーする")

8. ドキュメントの「**次の手順**」に従って、アプリにデータ、オフライン同期、認証、およびプッシュ通知を追加します。

    [![次のステップの手順を確認する](media/connected-services-image008-sml.png "次のステップの手順を確認する")](media/connected-services-image008.png#lightbox)

9. 既存のアプリケーション サービスがない場合、Visual Studio for Mac から新しいサービスを作成できます。
  サービス一覧の左下の **[新規]** ボタンをクリックして **[新しい App Service]** ダイアログを開きます。

    [![Visual Studio for Mac で新しいアプリ サービスを作成する](media/connected-services-image009-sml.png "Visual Studio for Mac で新しいアプリ サービスを作成する")](media/connected-services-image009.png#lightbox)

新しいサービスには以下のパラメーターが必要です。

- **App Service の名前**: プランに対して一意の名前/ID
- **サブスクリプション**: サービスの支払いに使用するサブスクリプション
- **リソース グループ**: プロジェクトでご利用のすべての Azure リソースを整理する方法。 既存のものを使用するか、新規作成するオプション。 これが初めての Azure サービスである場合、新規作成します。
- **サービス プラン**: それが使用されるすべてのリソースの場所とコストを決定する。 既存のものを使用するか、新規作成するオプション。 これが初めての Azure サービスである場合、既定のものを使用するか、無料プラン (F1) で新規作成します。

詳細については、「[Mobile Apps ドキュメント](/azure/app-service-mobile/)」を参照してください。

## <a name="see-also"></a>参照

- [接続済みサービス (Windows の Visual Studio)](/visualstudio/azure/vs-azure-tools-connected-services-storage)