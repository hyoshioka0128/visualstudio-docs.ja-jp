---
title: Visual Studio 管理者ガイド
titleSuffix: ''
description: エンタープライズ環境で Visual Studio を展開する方法について説明します。
ms.date: 06/02/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 9f4b044cddee59254e0b4f5198e75e3fa774aab7
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114213"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio 管理者ガイド

エンタープライズ環境では、システム管理者は一般的に、ネットワーク共有またはシステム管理ソフトウェアを使用してエンドユーザーにインストールを展開します。 エンタープライズ展開をサポートするために、Visual Studio セットアップ エンジンを設計しました。このエンジンにより、システム管理者はネットワーク インストールの場所を作成し、インストールの既定値を事前に構成したり、インストール プロセス中にプロダクト キーを展開したり、ロールアウトが成功した後に製品の更新プログラムを管理したりできます。

この管理者ガイドでは、ネットワーク環境でエンタープライズ展開を行うためのシナリオ ベースのガイダンスを示します。

## <a name="before-you-begin"></a>始める前に

組織全体に Visual Studio を展開する前に、いくつかの意思決定を行い、作業を完了する必要があります。

::: moniker range="vs-2019"

* 各ターゲット コンピューターで[最小インストール要件](/visualstudio/releases/2019/system-requirements/)が満たされていることを確認します。

* サービス ニーズについて決定します。

  会社がある機能セットを長く使用する必要があるが、定期的なサービス更新を取得する場合、サービス ベースラインの使用を計画します。 詳細については、「[Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers)」ページの「***Enterprise および Professional のお客様向けのサポート オプショ***」セクション、および「[サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)」ページをご覧ください。

  累積された機能更新と共にサービス更新を適用する予定の場合、最新の更新プログラムを選択できます。

* 更新モデルについて決定します。

  個々のクライアント コンピューターはどこから更新プログラムを入手しますか? 具体的には、更新プログラムをインターネットから取得するか、全社的なローカル共有から取得するかを決定します。 次に、ローカル共有を使用する場合、個々のユーザーが自分のクライアントを更新できるのか、管理者にプログラムでクライアントを更新してもらうのかを決定します。

* 会社に必要な[ワークロードとコンポーネント](workload-and-component-ids.md?view=vs-2019)を決定します。

* (スクリプト ファイルの詳細管理を簡単にする) [応答ファイル](automated-installation-with-response-file.md?view=vs-2019)を使用するかどうかを決定します。

* グループ ポリシーを有効にするかどうかと、個々のコンピューターで顧客フィードバックを無効にするように Visual Studio を構成するかどうかを決定します。

::: moniker-end

::: moniker range="vs-2017"

* 各ターゲット コンピューターで[最小インストール要件](/visualstudio/productinfo/vs2017-system-requirements-vs/)が満たされていることを確認します。

* サービス ニーズについて決定します。

  会社がある機能セットを長く使用する必要があるが、定期的なサービス更新を取得する場合、サービス ベースラインの使用を計画します。 詳細については、「[Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing#support-for-older-versions-of-visual-studio)」ページの「***旧バージョンの Visual Studio のサポート***」セクション、および「[サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)」ページをご覧ください。

  累積された機能更新と共にサービス更新を適用する予定の場合、最新の更新プログラムを選択できます。

* 更新モデルについて決定します。

  個々のクライアント コンピューターはどこから更新プログラムを入手しますか? 具体的には、更新プログラムをインターネットから取得するか、全社的なローカル共有から取得するかを決定します。 次に、ローカル共有を使用する場合、個々のユーザーが自分のクライアントを更新できるのか、管理者にプログラムでクライアントを更新してもらうのかを決定します。

* 会社に必要な[ワークロードとコンポーネント](workload-and-component-ids.md?view=vs-2017)を決定します。

* (スクリプト ファイルの詳細管理を簡単にする) [応答ファイル](automated-installation-with-response-file.md?view=vs-2017)を使用するかどうかを決定します。

* グループ ポリシーを有効にするかどうかと、個々のコンピューターで顧客フィードバックを無効にするように Visual Studio を構成するかどうかを決定します。

::: moniker-end

::: moniker range="vs-2019"

## <a name="step-1---download-visual-studio-product-files"></a>手順 1 - Visual Studio 製品ファイルをダウンロードする

* インストールする[ワークロードとコンポーネントを選択します](workload-and-component-ids.md?view=vs-2019)。

* [Visual Studio 製品ファイルのネットワーク共有を作成します](create-a-network-installation-of-visual-studio.md?view=vs-2019)。

## <a name="step-2---build-an-installation-script"></a>手順 2 - インストール スクリプトを作成する

* インストールを制御するために[コマンド ライン パラメーター](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019)を使用するインストール スクリプトを作成します。

  >[!NOTE]
  > [応答ファイル](automated-installation-with-response-file.md?view=vs-2019)を使用することでスクリプトを簡素化できます。 既定のインストール オプションを含む応答ファイルを必ず作成してください。

* (任意) インストール スクリプトの一部として[ボリューム ライセンスのプロダクト キーを適用](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2019)し、ユーザーがソフトウェアを個別にアクティブにする必要がないようにします。

* (任意) ネットワーク レイアウトを更新し、[エンドユーザーに製品の更新プログラムを配信するタイミングと場所を制御](controlling-updates-to-visual-studio-deployments.md?view=vs-2019)します。

* (任意) 他のバージョンまたはインスタンスと共有されている一部のパッケージがインストールされている場所、[パッケージがキャッシュされる場所](set-defaults-for-enterprise-deployments.md?view=vs-2019)、[パッケージがキャッシュされるかどうか](disable-or-move-the-package-cache.md?view=vs-2019)など、Visual Studio の展開に影響を与えるレジストリ ポリシーを設定します。

* (任意) グループ ポリシーを設定します。 個々のコンピューターで[顧客フィードバックを無効にするように Visual Studio を構成する](../ide/visual-studio-experience-improvement-program.md)こともできます。

## <a name="step-3---deploy"></a>手順 3 - 展開

* 任意の配置テクノロジを使用し、スクリプトをターゲットの開発者ワークステーションで実行します。

## <a name="step-4---deploy-updates"></a>手順 4 - 更新プログラムの展開

* 手順 1 で使用したコマンドを定期的に実行して更新されたコンポーネントを追加し、Visual Studio の[最新の更新プログラムを適用してネットワークの場所を更新](update-a-network-installation-of-visual-studio.md?view=vs-2019)します。

  更新スクリプトを使用して Visual Studio を更新できます。 それを行うには、[`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019) コマンドライン パラメーターを使用します。

## <a name="step-5---optional-use-visual-studio-tools"></a>手順 5 - (任意) Visual Studio ツールの使用

クライアント コンピューターに[インストールされている Visual Studio インスタンスを検出して管理する](tools-for-managing-visual-studio-instances.md?view=vs-2019)ために役立つ複数のツールが用意されています。

::: moniker-end

::: moniker range="vs-2017"

## <a name="step-1---download-visual-studio-product-files"></a>手順 1 - Visual Studio 製品ファイルをダウンロードする

* インストールする[ワークロードとコンポーネントを選択します](workload-and-component-ids.md?view=vs-2017)。

* [Visual Studio 製品ファイルのネットワーク共有を作成します](create-a-network-installation-of-visual-studio.md?view=vs-2017)。

## <a name="step-2---build-an-installation-script"></a>手順 2 - インストール スクリプトを作成する

* インストールを制御するために[コマンド ライン パラメーター](use-command-line-parameters-to-install-visual-studio.md?view=vs-2017)を使用するインストール スクリプトを作成します。

  >[!NOTE]
  > [応答ファイル](automated-installation-with-response-file.md?view=vs-2017)を使用することでスクリプトを簡素化できます。 既定のインストール オプションを含む応答ファイルを必ず作成してください。

* (任意) インストール スクリプトの一部として[ボリューム ライセンスのプロダクト キーを適用](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2017)し、ユーザーがソフトウェアを個別にアクティブにする必要がないようにします。

* (任意) ネットワーク レイアウトを更新し、[エンドユーザーに製品の更新プログラムを配信するタイミングと場所を制御](controlling-updates-to-visual-studio-deployments.md?view=vs-2017)します。

* (任意) 他のバージョンまたはインスタンスと共有されている一部のパッケージがインストールされている場所、[パッケージがキャッシュされる場所](set-defaults-for-enterprise-deployments.md?view=vs-2019)、[パッケージがキャッシュされるかどうか](disable-or-move-the-package-cache.md?view=vs-2017)など、Visual Studio の展開に影響を与えるレジストリ ポリシーを設定します。

* (任意) グループ ポリシーを設定します。 個々のコンピューターで[顧客フィードバックを無効にするように Visual Studio を構成する](../ide/visual-studio-experience-improvement-program.md)こともできます。

## <a name="step-3---deploy"></a>手順 3 - 展開

* 任意の配置テクノロジを使用し、スクリプトをターゲットの開発者ワークステーションで実行します。

## <a name="step-4---deploy-updates"></a>手順 4 - 更新プログラムの展開

* 手順 1 で使用したコマンドを定期的に実行して更新されたコンポーネントを追加し、Visual Studio の[最新の更新プログラムを適用してネットワークの場所を更新](update-a-network-installation-of-visual-studio.md?view=vs-2017)します。

  更新スクリプトを使用して Visual Studio を更新できます。 それを行うには、[`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019) コマンドライン パラメーターを使用します。

## <a name="step-5---optional-use-visual-studio-tools"></a>手順 5 - (任意) Visual Studio ツールの使用

クライアント コンピューターに[インストールされている Visual Studio インスタンスを検出して管理する](tools-for-managing-visual-studio-instances.md?view=vs-2017)ために役立つ複数のツールが用意されています。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [コマンド ライン パラメーターの例](command-line-parameter-examples.md)
* [Visual Studio オフライン インストールに必要な証明書をインストールする](install-certificates-for-visual-studio-offline.md)
* [インストール構成をインポートまたはエクスポートする](import-export-installation-configurations.md)
* [Visual Studio セットアップ アーカイブ](https://devblogs.microsoft.com/setup/tag/vs2017/)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
* [同期自動読み込みの設定](../extensibility/synchronously-autoloaded-extensions.md)
