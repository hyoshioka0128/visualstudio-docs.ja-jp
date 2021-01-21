---
title: Visual Studio 企業向けガイド
description: 企業環境で Visual Studio の設定とトラブルシューティングを行います。
ms.date: 07/29/2020
ms.custom: seodec18
ms.topic: overview
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: ''
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 56a6142d7217d6afa7d48ea708c642a32d8cb3c8
ms.sourcegitcommit: d97d72308ef306e7f28c3a76913caee4ff450bbb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2020
ms.locfileid: "90713439"
---
# <a name="visual-studio-enterprise-guide"></a>Visual Studio 企業向けガイド
お客様の会社で Visual Studio の利用を開始するときに時間を節約したい場合は、ここから開始してください。 この企業向けガイドには、一般的な企業シナリオにおいて Visual Studio をインストールおよび更新したり、問題が発生した場合にブロックを解除したり、さらにヘルプが必要な場合に問題を報告する方法を把握したりするためのヒントが含まれています。 

## <a name="get-started"></a>作業開始 
ネットワーク環境およびオフライン環境で、企業に Visual Studio を展開する方法について説明します。 

- **ネットワーク環境での企業向け展開のオプションについて理解します**。 「[Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)」には、システム管理者に向けたシナリオベースのガイダンスが記載されています。 

- **[トラブルシューティングのヒントを入手します](troubleshooting-installation-issues.md)** 。 Visual Studio をインストールまたは更新するときにヘルプを取得し、ブロックされている場合は問題を報告する方法を調べます。 これらのヒントには、オンラインまたはオフラインのインストールに関する問題のほとんどを解決できるステップ バイ ステップの手順が含まれています。 

- **[Visual Studio のオフライン インストールを作成します](create-an-offline-installation-of-visual-studio.md)** 。 インターネットに接続していない場合、またはインターネット接続が制限されている場合は、Visual Studio をインストールするためのオプションを検索します。 

- **[ブートストラップ パッケージを作成します](../deployment/creating-bootstrapper-packages.md)** 。 製品マニフェストとパッケージ マニフェストを作成してカスタム ブートストラップ パッケージを作成する方法について説明します。 

- **[Visual Studio の展開時にプロダクト キーを自動的に適用します](automatically-apply-product-keys-when-deploying-visual-studio.md)** 。 Visual Studio の配置を自動化するために使用されるスクリプトの一部として、プログラム的にプロダクト キーを適用することができます。 Visual Studio のインストール中、またはインストール完了後に、プログラムによってデバイスにプロダクト キーを設定できます。 

## <a name="install-visual-studio"></a>Visual Studio のインストール 

一般的な企業シナリオにおける Visual Studio のインストール方法について説明します。 

- **[コマンド ライン パラメーターを使用して Visual Studio をインストールします](use-command-line-parameters-to-install-visual-studio.md)** 。 各種パラメーターを使用して、Visual Studio のインストールを制御またはカスタマイズします。 インストール プロセスを自動化するか、後で使用するためにインストール ファイルのキャッシュを作成します。 

- **「[Visual Studio のインストールに使用するコマンド ライン パラメーターの例](command-line-parameter-examples.md)」をご覧ください**。 コマンド ライン パラメーターを使用して Visual Studio をインストールする方法を説明するため、いくつかの例が示されます。例は必要に応じてカスタマイズできます。 

- **[ファイアウォールまたはプロキシ サーバーの内側に Visual Studio および Azure サービスをインストールして使用します](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)** 。 お客様の組織でファイアウォールやプロキシ サーバーなどのセキュリティ対策が取られている場合は、Visual Studio および Azure サービスをインストールして使用する際に最良のエクスペリエンスを得るために、"許可リスト" への追加をお勧めするドメイン URL と、開くことをお勧めするポートおよびプロトコルがあります。 

- **[Visual Studio のネットワーク インストールを作成します](create-a-network-installation-of-visual-studio.md)** 。 初期インストールのファイルとすべての製品の更新プログラムを、単一のフォルダーにキャッシュします。  

## <a name="update-visual-studio"></a>Visual Studio を更新する 

Visual Studio を正常に更新し、更新に関する問題を修正する方法について説明します。 

- **[Visual Studio のネットワーク ベース インストールを更新します](update-a-network-installation-of-visual-studio.md)** 。 ネットワーク インストール レイアウトを Visual Studio の最新の更新プログラムのインストール ポイントとして使用できるように、また、クライアント ワークステーションに既に配置されているインストールを保持するために、最新の製品の更新プログラムを使って Visual Studio のネットワーク インストール レイアウトを更新します。

- **[サービス ベースライン使用時に Visual Studio を更新します](update-servicing-baseline.md)** 。 ベースラインでの更新の値を理解し、マイナー リリースとサービス更新プログラムの違いを学習します。 

- **[最小限のオフライン レイアウトを使用して Visual Studio を更新します](update-minimal-layout.md)** 。 インターネットに接続されていないコンピューターの場合、オフラインの Visual Studio インスタンスを更新する最も簡単かつ迅速な方法は、最小限のレイアウトを作成することです。

- **[Visual Studio を修復](repair-visual-studio.md)して更新プログラムの問題を修正します**。 Visual Studio のインストールが損傷したり、破損したりすることがあります。 修復は、更新プログラムを含め、すべてのインストール操作のインストール時の問題を解決するのに役立ちます。 

- **[Windows セキュリティ ベースライン](/windows/security/threat-protection/windows-security-baselines)に従います**。 Microsoft は、Windows 10 および Windows Server などのセキュリティで保護されたオペレーティング システムと、Microsoft Edge などのセキュリティで保護されたアプリなどをお客様に提供することに専念しています。 Microsoft は、製品のセキュリティ保証だけでなく、お客様にさまざまな構成機能を提供することで、ご利用環境のきめ細かい制御を可能にします。 

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目 

- [Visual Studio の生産性に関するガイド](../ide/productivity-features.md)