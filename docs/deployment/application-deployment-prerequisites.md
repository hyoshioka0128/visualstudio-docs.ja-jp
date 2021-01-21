---
title: アプリケーション配置の前提条件 |Microsoft Docs
description: '[必須コンポーネント] ダイアログボックスとブートストラップパッケージの使用など、アプリケーションの展開の前提条件について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, platform detection
- ClickOnce deployment, prerequisites
- ClickOnce deployment, dependencies
- prerequisites, ClickOnce
- dependencies, ClickOnce
ms.assetid: fc6e047e-ad94-44e8-8ff5-b6d1f4ca7735
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c87b0f6ded2960054cb553dbeb85681aa447668b
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94383249"
---
# <a name="application-deployment-prerequisites"></a>アプリケーション配置の必要条件

アプリケーションを正常にインストールして実行するには、まず、アプリケーションが依存するすべてのコンポーネントを対象のコンピューターにインストールします。 たとえば、を使用して作成されたほとんどのアプリケーションは、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .NET Framework に依存しています。 この場合、アプリケーションをインストールする前に、適切なバージョンの共通言語ランタイムが対象コンピューターに存在している必要があります。

 [ **必須コンポーネント] ダイアログボックス** でこれらの必須コンポーネントを選択し、インストールの一部として .NET Framework とその他の再頒布可能パッケージをインストールすることができます。 この方法は *ブートストラップ* と呼ばれます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]*Setup.exe* という名前の Windows 実行可能プログラムを生成します。これは *ブートストラップ* とも呼ばれます。 ブートストラップは、アプリケーションが実行される前にこれらの必須コンポーネントをインストールします。 これらの前提条件の選択の詳細については、「[ [必須コンポーネント] ダイアログボックス](../ide/reference/prerequisites-dialog-box.md)」を参照してください。

 各必須コンポーネントはブートストラップ パッケージです。 ブートストラップパッケージは、前提条件のインストール方法を記述したマニフェストファイルを含むディレクトリとファイルのグループです。 アプリケーションの必須コンポーネントが **[必須コンポーネント]** ダイアログ ボックスに表示されない場合は、カスタム ブートストラップ パッケージを作成して Visual Studio に追加できます。 それにより、 **[必須コンポーネント]** ダイアログ ボックスで必須コンポーネントを選択できるようになります。 詳細については、「 [ブートストラップパッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。

 既定では、ブートストラップは ClickOnce の配置で有効です。 ClickOnce の配置に生成されるブートストラップは署名付きです。 コンポーネントのブートストラップを無効にすることができますが、正しいバージョンのコンポーネントがすべての対象コンピューターに既にインストールされていることを確認してください。

## <a name="bootstrapping-and-clickonce-deployment"></a>ブートストラップと ClickOnce 配置
 クライアントコンピューターにアプリケーションをインストールする前に、はクライアントを調べて、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェストに要件が指定されていることを確認します。 次の要件があります。

- 最低限必要な共通言語ランタイムのバージョン。これはアプリケーション マニフェストにアセンブリ依存関係として指定されます。

- アプリケーションに最低限必要な Windows オペレーティング システムのバージョン。これは、アプリケーション マニフェストに `<osVersionInfo>` 要素を使用して指定されます。 (「 [ \<dependency> Element](../deployment/dependency-element-clickonce-application.md)」を参照してください)。

- アセンブリマニフェストのアセンブリ依存関係宣言で指定されているように、グローバルアセンブリキャッシュ (GAC) にプレインストールする必要があるすべてのアセンブリの最小バージョン。

  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不足している前提条件を検出し、ブートストラップを使用して必須コンポーネントをインストールすることができます。 詳細については、「 [方法: ClickOnce アプリケーションを使用して必須コンポーネントをインストール](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)する」を参照してください。

> [!NOTE]
> やMageUI.exeなどのツールによって生成されるマニフェストの値を変更するには、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] テキストエディターでアプリケーションマニフェストを編集し、アプリケーションマニフェストと配置マニフェストの両方に再署名する必要があります。 ** 詳細については、「 [方法: アプリケーションマニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)する」を参照してください。

 Visual Studio と ClickOnce を使用してアプリケーションを配置する場合、既定で選択されるブートストラップ パッケージは、ソリューション内の .NET Framework のバージョンによって異なります。 ただし、対象の .NET Framework のバージョンを変更する場合は、 **[必須コンポーネント]** ダイアログ ボックスのオプションを手動で更新する必要があります。

|対象の .NET Framework|選択されるブートストラップ パッケージ|
|---------------------------|------------------------------------|
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows インストーラー 3.1|
|.NET Framework 4|.NET Framework 4<br /><br /> Windows インストーラー 3.1|

 配置では [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、発行ウィザードによって生成される *Publish.htm* ページ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、アプリケーションのみをインストールするリンク、またはアプリケーションとブートストラップコンポーネントの両方をインストールするリンクのいずれかを指します。

 ClickOnce 発行ウィザードまたは Visual Studio の [発行] ページを使用してブートストラップを生成した場合、 *Setup.exe* は自動的に署名されます。 ただし、顧客の証明書を使用してブートストラップに署名する場合は、後でファイルに署名できます。

## <a name="bootstrapping-and-msbuild"></a>ブートストラップと MSBuild
 を使用せず [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、コマンドラインでアプリケーションをコンパイルする場合は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] Microsoft Build Engine (MSBuild) タスクを使用してブートストラップアプリケーションを作成できます。 詳細については、「 [Generatebootstrapper タスク](../msbuild/generatebootstrapper-task.md)」を参照してください。

 ブートストラップの代わりに、Microsoft SMS (Systems Management Server) などの電子ソフトウェア配布システムを使用して、コンポーネントを事前に配置することもできます。

## <a name="bootstrapper-setupexe-command-line-arguments"></a>ブートストラップ (Setup.exe) のコマンド ライン引数
 によって生成される *Setup.exe* [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と MSBuild タスクは、次のコマンドライン引数セットをサポートしています。 その他の引数は、アプリケーションインストーラーに転送されます。

 ブートストラップオプションを変更する場合は、署名されていないブートストラップを変更し、後でブートストラップファイルに署名する必要があります。

| コマンドライン引数 | [説明] |
| - | - |
| **-?、-h、-help** | [ヘルプ] ダイアログ ボックスを表示します。 |
| **-url、-componentsurl** | このセットアップ用に保存されている URL とコンポーネントの URL を表示します。 |
| **-url =**`location` | *Setup.exe* がアプリケーションを検索する場所の URL を設定し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 |
| **-componentsurl=** `location` | *Setup.exe* が依存関係 (.NET Framework など) を検索する URL を設定します。 |
| **-homesite=** `true` **&#124;** `false` | `true`の場合、は、ベンダーのサイトの適切な場所から依存関係をダウンロードします。 この設定は、 **-の url** 設定よりも優先されます。 の場合 `false` 、 **-コンポーネント url** で指定された url から依存関係をダウンロードします。 |

## <a name="operating-system-support"></a>オペレーティング システムのサポート
 Visual Studio ブートストラップは、Windows Server 2008 Server Core または Windows Server 2008 R2 Server Core ではサポートされていません。これは、機能が制限された低メンテナンスのサーバー環境を提供するためです。 たとえば、Server Core インストールオプションでサポートされているのは、.NET Framework 3.5 Server Core profile だけで、完全な .NET Framework に依存する Visual Studio 機能を実行することはできません。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)