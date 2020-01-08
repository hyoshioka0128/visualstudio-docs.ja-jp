---
title: 自動テストに Azure Pipelines を使用する
ms.date: 10/19/2018
ms.topic: conceptual
helpviewer_keywords:
- automated testing, lab management, test lab
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: bd6e9b2d9ea408e451b7032a00c3c96fb0ef2b58
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75566827"
---
# <a name="use-azure-test-plans-instead-of-lab-management-for-automated-testing"></a>自動化されたテストに Lab Management ではなく Azure Test Plans を使用する

このトピックでは、テストの自動化または、ビルド、配置、テストの自動化に Microsoft Test Manager と Lab Management を使用している場合に、Azure Pipelines および Team Foundation Server (TFS) の[ビルドとリリース](/azure/devops/pipelines/index?view=vsts)機能を使用して同じ目的を達成する方法を説明します。

## <a name="build-deploy-test-automation"></a>ビルド、配置、テストの自動化

Microsoft Test Manager と Lab Management は、アプリケーションのビルド、配置、テストの自動化に XAML のビルド定義に依存しています。 XAML ビルドは、目的の達成に、ラボ環境、テスト スイート、テストの設定など Microsoft Test Manager で作成されたさまざまな構造および、ビルド コントローラー、ビルド エージェント、テスト コントローラー、テスト エージェントなどのさまざまなインフラストラクチャ コンポーネントに依存しています。 Azure Pipelines または TFS を使用すると、同じことを少ない手順で達成することができます。

| 手順 | XAML ビルドを使用する場合 | ビルドまたはリリースを使用する場合 |
|-------|----------------------|-----------------|
| ビルドを展開してテストを実行するマシンを特定します。 | それらのマシンの Microsoft Test Manager に標準のラボ環境を作成します。 | N/A |
| 実行するテストを特定します。 | Microsoft Test Manager にテスト スイートを作成し、テスト ケースを作成し、各テスト ケースと自動化を関連付けます。 テストを実行するラボ環境のマシンのロールを指定し、Microsoft Test Manager でテスト設定を作成します。 | テスト計画でテストを管理する計画である場合、Microsoft Test Manager に同じように自動化されたテスト スイートを作成します。 または、ビルドで生成されたテスト バイナリから直接テストを実行する場合は、これを省略することが可能です。 いずれの場合もテスト設定を作成する必要はありません。 |
| 配置とテストを自動化します。 | LabDefaultTemplate.*.xaml を使用し、XAML ビルド定義を作成します。 ビルド定義に、ビルド、テスト スイートおよびラボ環境を指定します。 | 1 つの環境の[ビルドまたはリリース パイプライン](/azure/devops/pipelines/index?view=vsts)を作成します。 コマンド ライン タスクを使用して (XAML ビルド定義から) 同じ配置スクリプトを実行し、Test Agent の配置と機能テストの実行タスクを使用して自動化されたテストを実行します。 これらのタスクにマシンの一覧とその資格情報を入力し指定します。 |

このシナリオで Azure Pipelines または TFS を使用する利点は次のとおりです。

* ビルド コントローラーまたはテスト コントローラーが不要です。
* テスト エージェントはビルドまたはリリースの一部としてタスクでインストールされます。
* 配置の手順を簡単にカスタマイズできます。 1 つのスクリプトの使用のみに限定されなくなります。 この製品および Visual Studio Marketplace で使用可能な多数のタスクも利用できます。
* テスト スイートを維持する必要がありません。 バイナリから直接テストを実行できます。
* 各ビルドまたはリリース内で実行されたテストのより充実したインライン レポートを得ることができます。
* 各環境に現在配置され、テストされている資産 (リリース、ビルド、作業項目、コミット) を追跡できます。
* 自動化をカスタマイズして拡張し、複数のテスト環境や運用環境にも簡単に展開できるようになります。
* 自動化は、チェックインやコミットがあった場合、または特定の時刻に毎日行われるようスケジュールできます。

## <a name="self-service-management-of-scvmm-environments"></a>SCVMM 環境のセルフ サービスの管理

[Microsoft Test Manager のテスト センター](/azure/devops/test/mtm/guidance-mtm-usage?view=vsts)では、環境テンプレートのライブラリを管理する機能をサポートしたり、[SCVMM サーバー](/system-center/vmm/overview?view=sc-vmm-1801)を使用したオンデマンドでの環境のプロビジョニングをサポートしたりしています。

ラボ センターのセルフ サービス プロビジョニング機能には、次の 2 つの明確な目標があります。

* 簡単にインフラストラクチャを管理できるようにします。 VM と環境テンプレートを管理し、環境の個々のクローンを分離するプライベート ネットワークを自動的に作成することがインフラストラクチャの管理の例です。

* チームでテストと配置を行っている場合、より単純に仮想マシンが使えるようになります。 同じプロジェクト セキュリティ モデルでラボ環境にアクセスできるようにすることと、テスト シナリオでそれらの仮想マシンを統合して使用できるようにすることが使いやすさの一例です。

ただし、[Microsoft Azure](https://azure.microsoft.com/) や [Microsoft Azure Stack](https://azure.microsoft.com/overview/azure-stack/) などのより充実したパブリック クラウドおよびプライベート クラウド システムの進化のため、TFS 2017 以降のインフラストラクチャの管理機能には進展がありません。 代わりに、それらのクラウド インフラストラクチャで管理されるリソースを使いやすくする取り組みは継続されています。

次の表では、ラボ センターで実行する一般的なアクティビティと、それを (インフラストラクチャを管理するアクティビティの場合) SCVMM または Azure で、または (テストおよび配置アクティビティの場合) TFS と Azure DevOps Services で実行する方法をまとめています。

| 手順 | ラボ センターを使用する場合 | ビルドまたはリリースを使用する場合 |
|-------|-----------------|-----------------------|
| 環境テンプレートのライブラリを管理します。 | ラボ環境を作成します。 仮想マシンに必要なソフトウェアをインストールします。 Sysprep を実行し、ライブラリに環境をテンプレートとして格納します。 | SCVMM 管理コンソールを直接使用して、仮想マシン テンプレートまたはサービス テンプレートのいずれかを作成および管理します。 Azure を使用する場合は、[Azure クイックスタート テンプレート](https://azure.microsoft.com/resources/templates/)のいずれかを選択します。 |
| ラボ環境を作成します。 | ライブラリで環境テンプレートを選択し、それを配置します。 必要なパラメーターを入力し、仮想マシンの構成をカスタマイズします。 | SCVMM 管理コンソールを使用すると、テンプレートから VM またはサービス インスタンスを直接作成できます。 リソースを作成するには、Azure Portal を直接使用します。 または、環境のリリース定義を作成します。 [SCVMM Integration の拡張機能](https://marketplace.visualstudio.com/items?itemname=ms-vscs-rm.scvmmapp)の Azure のタスクを使用し、新しい仮想マシンを作成します。 この定義の新しいリリースの作成は、ラボ センターで新しい環境を作成することと同じです。 |
| マシンに接続します。 | 環境ビューアーでラボ環境を開きます。 | 仮想マシンに接続するために、SCVMM 管理コンソールを直接使用します。 または、仮想マシンの IP アドレスまたは DNS 名を使用して、リモート デスクトップ セッションを開きます。 |
| 環境のチェックポイントを取得するか、クリーンなチェックポイントに環境を復元します。 | 環境ビューアーでラボ環境を開きます。 チェックポイントを取得するまたは前のチェックポイントに復元するオプションを選択します。 | 仮想マシンでこれらの操作を実行するために、直接 SCVMM 管理コンソールを使用します。 または、これらの手順をより大規模な自動化の一環として実行するには、リリース定義の環境の一部として [SCVMM Integration 拡張機能](https://marketplace.visualstudio.com/items?itemname=ms-vscs-rm.scvmmapp)からチェックポイント タスクを含めます。 |

## <a name="create-network-isolated-environments"></a>ネットワークが分離された環境を作成する

ネットワークが分離されたラボ環境とは、ネットワークの競合を引き起こすことがなく安全に複製できる SCVMM 仮想マシンのグループです。 これは、MTM で、一連のネットワーク インターフェイス カードを使用してプライベート ネットワークに仮想マシンを構成した、および別の一連のネットワーク インターフェイス カードを使用してパブリック ネットワークに仮想マシンを構成した一連の手順で行われました。

ただし、Azure Pipelines と TFS を SCVMM ビルドおよび配置タスクと組み合わせて使うことで、SCVMM 環境の管理、分離仮想ネットワークのプロビジョニング、およびビルド、配置、テスト シナリオの実装を行うことができます。 たとえば、タスクを使って次のことができます。

* チェックポイントを作成、復元、削除する
* テンプレートを使って新しい仮想マシンを作成する
* 仮想マシンを開始および停止する
* SCVMM のカスタム PowerShell スクリプトを実行する

詳細については、「[Create a virtual network isolated environment for build-deploy-test scenarios](/azure/devops/pipelines/targets/create-virtual-network?view=vsts)」(ビルド、配置、テスト シナリオのための仮想ネットワーク分離環境を作成する) を参照してください。
