---
title: ClickOnce のセキュリティと配置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployment
- deploying applications [ClickOnce]
- ClickOnce deployment
- publishing, ClickOnce
ms.assetid: abab6d34-c3c2-45c1-a8b6-43c7d3131e7a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d33e99d11007ca4684f3d875620e2baeb7ddc1e7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285495"
---
# <a name="clickonce-security-and-deployment"></a>ClickOnce のセキュリティと配置
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]は、ユーザーの介入を最小限に抑えてインストールして実行できる、自己更新型の Windows ベースのアプリケーションを作成できるようにする展開テクノロジです。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]Visual Basic および Visual C# を使用してプロジェクトを開発した場合は、ClickOnce テクノロジを使用して配置されたアプリケーションの発行と更新を完全にサポートします。 Visual C++ アプリケーションの配置の詳細については、「 [Visual C++ アプリケーションの ClickOnce 配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)」を参照してください。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]展開では、次の3つの主要な問題を克服できます。

- **アプリケーションの更新における問題。** Microsoft Windows インストーラーの展開では、アプリケーションが更新されるたびに、ユーザーは更新プログラムと msp ファイルをインストールし、インストールされている製品に適用することができます。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]配置では、更新プログラムを自動的に提供できます。 アプリケーションの変更された部分のみがダウンロードされ、更新された完全なアプリケーションが新しいサイドバイサイドフォルダーから再インストールされます。

- **ユーザーのコンピューターへの影響。** Windows インストーラーの展開では、アプリケーションは共有コンポーネントに依存し、バージョン管理の競合が発生する可能性があります。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]配置では、各アプリケーションは自己完結型であり、他のアプリケーションと干渉することはできません。

- **セキュリティのアクセス許可。** Windows インストーラーの展開には管理アクセス許可が必要であり、限られたユーザーインストールのみが許可されます。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]展開により、管理者以外のユーザーは、アプリケーションに必要なコードアクセスセキュリティのアクセス許可のみをインストールして付与することができます。

  これまで、これらの問題は、開発を容易にするために、開発者が Windows ベースのアプリケーションではなく Web アプリケーションを作成することにした場合に発生することがありました。 を使用して展開されたアプリケーションを使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] すると、両方のテクノロジを最大限に活用できます。

## <a name="what-is-a-clickonce-application"></a>ClickOnce アプリケーションとは
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションとは、テクノロジを使用して公開された Windows Presentation Foundation (*xbap*)、Windows フォーム (*.exe*)、コンソールアプリケーション (*.exe*)、または Office ソリューション (*.dll*) です。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] Web ページ、ネットワークファイル共有、または cd-rom などのメディアから、3つの異なる方法で公開できます。 アプリケーションは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] エンドユーザーのコンピューターにインストールし、コンピューターがオフラインのときでもローカルで実行することができます。また、エンドユーザーのコンピューターに永続的にインストールすることなく、オンライン専用モードで実行することもできます。 詳細については、「 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションを自己更新することができます。新しいバージョンが利用可能になったことを確認し、更新されたファイルを自動的に置き換えます。 開発者は、更新動作を指定できます。また、ネットワーク管理者は、更新を必須としてマークするなど、更新方法を制御することもできます。 更新プログラムは、エンドユーザーまたは管理者によって以前のバージョンにロールバックすることもできます。 詳細については、「 [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

 アプリケーション [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] が分離されているため、アプリケーションをインストールまたは実行しても、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 既存のアプリケーションを中断することはできません。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションは自己完結型です。各 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、セキュリティで保護されたユーザーごとのアプリケーションごとのキャッシュにインストールされ、実行されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションは、インターネットまたはイントラネットのセキュリティゾーンで実行されます。 必要であれば、アプリケーションから昇格されたセキュリティ アクセス許可を要求できます。 詳細については、「[セキュリティで保護された ClickOnce アプリケーション](../deployment/securing-clickonce-applications.md)」を参照してください。

## <a name="how-clickonce-security-works"></a>ClickOnce セキュリティのしくみ
 コア [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] セキュリティは、証明書、コードアクセスセキュリティポリシー、および ClickOnce 信頼プロンプトに基づいています。

### <a name="certificates"></a>証明書
 Authenticode 証明書は、アプリケーションの発行元の信頼性を検証するために使用されます。 ClickOnce は、アプリケーションの配置に Authenticode を使用することによって、確立された信頼できるソースから取得される正当なプログラムとして有害なプログラムが人々を防ぐのに役立ちます。 必要に応じて、証明書を使用してアプリケーションマニフェストと配置マニフェストに署名し、ファイルが改ざんされていないことを証明することもできます。 詳細については、「 [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。 証明書を使用して、信頼された発行元の一覧を持つようにクライアントコンピューターを構成することもできます。 アプリケーションが信頼された発行元からのものである場合は、ユーザーの操作なしでインストールできます。 詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

### <a name="code-access-security"></a>コード アクセス セキュリティ
 コードアクセスセキュリティは、保護されたリソースに対するコードのアクセスを制限するのに役立ちます。 ほとんどの場合、インターネットまたはローカルのイントラネットゾーンを選択してアクセス許可を制限できます。 **Projectdesigner**の [**セキュリティ**] ページを使用して、アプリケーションに適切なゾーンを要求します。 アクセス許可が制限されたアプリケーションをデバッグして、エンドユーザーエクスペリエンスをエミュレートすることもできます。 詳細については、「 [ClickOnce アプリケーションのコードアクセスセキュリティ](../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

### <a name="clickonce-trust-prompt"></a>ClickOnce 信頼プロンプト
 アプリケーションがゾーンよりも多くのアクセス許可を要求した場合、エンドユーザーに対して信頼の決定を求めるメッセージが表示されます。 エンドユーザーは、Windows フォームアプリケーション、Windows Presentation Foundation アプリケーション、コンソールアプリケーション、XAML ブラウザーアプリケーション、Office ソリューションなどの ClickOnce アプリケーションの実行が信頼されているかどうかを判断できます。 詳細については、「[方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)」を参照してください。

## <a name="how-clickonce-deployment-works"></a>ClickOnce 配置のしくみ
 コア [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置アーキテクチャは、アプリケーションマニフェストと配置マニフェストの2つの XML マニフェストファイルに基づいています。 ファイルは、ClickOnce アプリケーションのインストール元、更新方法、および更新日時を記述するために使用されます。

### <a name="publish-clickonce-applications"></a>ClickOnce アプリケーションの発行
 アプリケーションマニフェストには、アプリケーション自体が記述されています。 これには、アセンブリ、アプリケーションを構成する依存関係とファイル、必要なアクセス許可、および更新プログラムが使用可能になる場所が含まれます。 アプリケーション開発者は、Visual Studio の発行ウィザードまたはのマニフェスト生成および編集ツール (*Mage.exe*) を使用して、アプリケーションマニフェストを作成し [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] ます。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。

 配置マニフェストでは、アプリケーションの配置方法を示します。 これには、アプリケーションマニフェストの場所と、クライアントが実行する必要があるアプリケーションのバージョンが含まれます。

### <a name="deploy-clickonce-applications"></a>ClickOnce アプリケーションの配置
 配置マニフェストを作成したら、それを配置場所にコピーします。 配置場所は、Web サーバー、ネットワーク ファイル共有、CD などのメディアのいずれでもかまいません。 アプリケーションマニフェストとすべてのアプリケーションファイルは、配置マニフェストで指定された配置場所にもコピーされます。 これは、配置場所と同じ場所でも、別の場所でもかまいません。 Visual Studio で**発行ウィザード**を使用する場合、コピー操作は自動的に実行されます。

### <a name="install-clickonce-applications"></a>ClickOnce アプリケーションのインストール
 配置場所に配置されたら、エンド ユーザーは Web ページ上またはフォルダー内の配置マニフェスト ファイルを表すアイコンをクリックすることで、アプリケーションをダウンロードしてインストールできます。 ほとんどの場合、エンドユーザーには、インストールの確認を求める簡単なダイアログボックスが表示されます。インストールが完了すると、追加の操作を行わずにアプリケーションが起動します。 アプリケーションに昇格されたアクセス許可が必要な場合、またはアプリケーションが信頼された証明書によって署名されていない場合、ダイアログボックスでは、インストールを続行する前にアクセス許可を付与するようにユーザーに求めます。 ClickOnce のインストールはユーザー単位ですが、管理者特権を必要とする前提条件がある場合は、アクセス許可の昇格が必要になることがあります。 高度なアクセス許可の詳細については、「 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)」を参照してください。

 証明書はコンピューターレベルまたはエンタープライズレベルで信頼できます。これにより、信頼された証明書で署名された ClickOnce アプリケーションをサイレントインストールできます。 信頼できる証明書の詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

 アプリケーションは、ユーザーの [**スタート**] メニューと、**コントロールパネル**の [**プログラムの追加と削除**] グループに追加できます。 他の展開テクノロジとは異なり、 **Program Files**フォルダーまたはレジストリには何も追加されず、インストールに管理者権限は必要ありません。

> [!NOTE]
> また、アプリケーションを [**スタート**] メニューに追加したり、[プログラムの**追加と削除**] グループを削除したりすると、Web アプリケーションのように動作するようになります。 詳細については、「 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

### <a name="update-clickonce-applications"></a>ClickOnce アプリケーションを更新する
 アプリケーション開発者は、アプリケーションの更新されたバージョンを作成すると、新しいアプリケーションマニフェストを生成し、ファイルを配置場所 (通常は、元のアプリケーション配置フォルダーの兄弟フォルダー) にコピーします。 管理者は、アプリケーションの新しいバージョンの場所を示すために配置マニフェストを更新します。

> [!NOTE]
> これらの手順は、Visual Studio の**発行ウィザード**を使用して実行できます。

 配置マニフェストには、配置場所だけでなく、アプリケーションで最新バージョンをチェックする更新場所 (Web ページまたはネットワーク ファイル共有) も含まれます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]**発行**プロパティは、アプリケーションが更新プログラムを確認するタイミングと頻度を指定するために使用されます。 更新動作は、配置マニフェストで指定することも、api を使用してアプリケーションのユーザーインターフェイスでユーザーの選択として表示することもでき [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 さらに、**[発行]** プロパティを使用して、更新を必須にしたり、以前のバージョンにロールバックしたりすることもできます。 詳細については、「 [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

### <a name="third-party-installers"></a>サードパーティのインストーラー
 ClickOnce インストーラーをカスタマイズして、アプリケーションと共にサードパーティのコンポーネントをインストールできます。 再頒布可能パッケージ (.exe または .msi ファイル) があり、言語に依存しない製品マニフェストと言語固有のパッケージマニフェストを含むパッケージについて記述している必要があります。 詳細については、「[ブートストラップパッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。

## <a name="clickonce-tools"></a>ClickOnce ツール
 次の表は、アプリケーションマニフェストと配置マニフェストの生成、編集、署名、および再署名に使用できるツールを示しています。

|ツール|説明|
|----------|-----------------|
|[[セキュリティ] ページ (プロジェクト デザイナー)](../ide/reference/security-page-project-designer.md)|アプリケーションマニフェストと配置マニフェストに署名します。|
|[[発行] ページ (プロジェクトデザイナー)](../ide/reference/publish-page-project-designer.md)|Visual Basic および Visual C# アプリケーションのアプリケーションマニフェストおよび配置マニフェストを生成して編集します。|
|[*Mage.exe* (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)|Visual Basic、Visual C#、および Visual C++ アプリケーションのアプリケーションマニフェストと配置マニフェストを生成します。<br /><br /> アプリケーションマニフェストと配置マニフェストに署名し、再署名します。<br /><br /> バッチスクリプトとコマンドプロンプトから実行できます。|
|[*MageUI.exe* (マニフェスト生成および編集ツール、グラフィカルクライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)|アプリケーションマニフェストと配置マニフェストを生成して編集します。<br /><br /> アプリケーションマニフェストと配置マニフェストに署名し、再署名します。|
|[GenerateApplicationManifest タスク](../msbuild/generateapplicationmanifest-task.md)|アプリケーションマニフェストを生成します。<br /><br /> MSBuild から実行できます。 詳細については、「 [MSBuild リファレンス](../msbuild/msbuild-reference.md)」を参照してください。|
|[GenerateDeploymentManifest タスク](../msbuild/generatedeploymentmanifest-task.md)|配置マニフェストを生成します。<br /><br /> MSBuild から実行できます。 詳細については、「 [MSBuild リファレンス](../msbuild/msbuild-reference.md)」を参照してください。|
|[SignFile タスク](../msbuild/signfile-task.md)|アプリケーションマニフェストと配置マニフェストに署名します。<br /><br /> MSBuild から実行できます。 詳細については、「 [MSBuild リファレンス](../msbuild/msbuild-reference.md)」を参照してください。|
|[Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/microsoft.build.tasks.deployment.manifestutilities)|独自のアプリケーションを開発して、アプリケーションマニフェストと配置マニフェストを生成します。|

 次の表は、これらのブラウザーで ClickOnce アプリケーションをサポートするために必要な .NET Framework バージョンを示しています。

|ブラウザー|.NET Framework のバージョン|
|-------------|----------------------------|
|Internet Explorer|2.0、3.0、3.5、3.5 SP1、4|
|Firefox|2.0 SP1、3.5 SP1、4|
|Chrome|3.5|
|Microsoft Edge|3.5|

## <a name="see-also"></a>関連項目
- [Windows Vista の ClickOnce 配置](../deployment/clickonce-deployment-on-windows-vista.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce での COM コンポーネントの配置](../deployment/deploying-com-components-with-clickonce.md)
- [ClickOnce アプリケーションのコマンド ラインからのビルド](../deployment/building-clickonce-applications-from-the-command-line.md)
- [アプリケーションを使用する ClickOnce アプリケーションをデバッグする](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)
