---
title: Office ソリューションの配置のトラブルシューティング
description: Office ソリューションを配置するときに発生する可能性のある一般的な問題を解決する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- Office development in Visual Studio, troubleshooting
- deploying applications [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b70b03e8342564de828059d1a335f6347c19b5a3
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97522976"
---
# <a name="troubleshoot-office-solution-deployment"></a>Office ソリューションの配置のトラブルシューティング
  このトピックでは、Office ソリューションを配置するときに発生する可能性がある一般的な問題を解決する方法について説明します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="troubleshoot-office-solutions-by-using-the-event-viewer"></a>イベントビューアーを使用した Office ソリューションのトラブルシューティング
 Windows のイベント ビューアーを使用すると、Office ソリューションのインストール時またはアンインストール時に [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] でキャプチャされるエラー メッセージを表示できます。 イベント ロガーからのこれらのメッセージを使用して、インストールと配置の問題を解決できます。 詳細については、「 [Office ソリューションのイベントログ](../vsto/event-logging-for-office-solutions.md)」を参照してください。

## <a name="change-the-assembly-name-causes-conflicts"></a>アセンブリ名を変更すると競合が発生する
 ソリューションを配置した後に **プロジェクトデザイナー** の [**アプリケーション**] ページで [**アセンブリ名**] の値を変更すると、発行ツールによって、1つの *Setup.exe* ファイルと2つの配置マニフェストを含むセットアップパッケージが変更されます。 2 つのマニフェスト ファイルを配置すると、次のような状況が発生する場合があります。

- エンド ユーザーが両方のバージョンをインストールすると、アプリケーションは両方の VSTO アドインを読み込みます。

- VSTO アドインがインストールされている状態でアセンブリの名前を変更すると、エンド ユーザーが更新を受け取ることはなくなります。

  このような状況を回避するには、ソリューションを配置した後で、ソリューションの **アセンブリ名** の値を変更しないでください。

## <a name="check-for-updates-takes-a-long-time"></a>更新プログラムの確認に長い時間がかかる
 Visual Studio 2010 Tools for Office runtime には、管理者がマニフェストとソリューションをダウンロードするためのタイムアウト値を設定するために使用できるレジストリエントリが用意されています。

#### <a name="to-set-the-time-out-value"></a>タイムアウト値を設定するには

1. レジストリで、次のキーに移動します。

     **HKEY_CURRENT_USER\Software\Microsoft\VSTA**

2. **AddInTimeout** サブキーに、タイムアウト値をミリ秒単位で設定します。

     **[AddInTimeout]** サブキーが存在しない場合は、DWORD として作成します。

## <a name="cant-update-or-publish-to-a-network-file-share"></a>ネットワークファイル共有に更新または発行できません
 ネットワークファイル共有上の Office ソリューションでは、更新の発行中にソリューションの *Setup.exe* ファイルがロックされている場合、更新中に誤解を招くメッセージが表示されることがあります。 たとえば、"'setup.exe' を Web サイトに追加できません。 ファイル 'setup.exe' はこの Web サイトに既に存在します。" というメッセージが表示されることがあります。

 ファイルがロックされないようにするには、エンド ユーザーに対して共有を読み取り専用に設定します。 ただし、共有上にドキュメントがあると、このドキュメントもエンド ユーザーに対して読み取り専用になります。

## <a name="prerequisites-for-microsoft-office-arent-installed"></a>Microsoft Office の前提条件がインストールされていません
 セットアップ パッケージには、Office ソリューションと共に配置される必須コンポーネントとして、.NET Framework、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]、および Office プライマリ相互運用機能アセンブリを追加できます。 プライマリ相互運用機能アセンブリをインストールする方法の詳細については、「 [office ソリューションを開発するためのコンピューターの構成](../vsto/configuring-a-computer-to-develop-office-solutions.md) 」および「 [方法: office プライマリ相互運用機能アセンブリをインストール](../vsto/how-to-install-office-primary-interop-assemblies.md)する」を参照してください。

## <a name="publish-using-localhost-can-cause-installation-problems"></a>Localhost を使用して発行すると、インストールの問題が発生することがある
 `http://localhost`ドキュメントレベルのソリューションの発行場所またはインストール先としてを使用すると、**発行ウィザード** によって文字列が実際のコンピューター名に変換されることはありません。 この場合は、ソリューションを開発用コンピューター上にインストールする必要があります。 配置ソリューションに開発用コンピューター上の IIS を使用させるには、HTTP、HTTPS、FTP のすべての場所について、localhost ではなく完全修飾名を使用します。

## <a name="cached-assemblies-are-loaded-instead-of-updated-assemblies"></a>更新されたアセンブリではなく、キャッシュされたアセンブリが読み込まれる
 プロジェクトの出力パスがネットワーク ファイル共有上にあり、アセンブリが厳密な名前で署名されていて、カスタマイズ アセンブリのバージョンが変更されていない場合、.NET Framework アセンブリ ローダーである fusion は、キャッシュしたアセンブリのコピーを読み込みます。 アセンブリを更新しても、これらの条件が満たされるとキャッシュしたコピーが読み込まれるため、プロジェクトを次回実行するときに更新は表示されません。

 Visual Studio を構成し、プロジェクトを実行するたびに fusion がアセンブリをダウンロードするように設定できます。

### <a name="to-download-assemblies-instead-of-loading-cached-copies"></a>キャッシュしたコピーではなくアセンブリをダウンロードするには

1. メニュー バーで、 **[プロジェクト]**、[ _ProjectName_**のプロパティ]**」を参照してください。

2. **[アプリケーション]** ページで、 **[アセンブリ情報]** を選択します。

3. **アセンブリのバージョン** のリビジョン番号、3番目のフィールドをワイルドカード () に設定し \* ます。 たとえば、"1.0. *" のようになります。  次に、[ **OK** ] をクリックします。

   アセンブリのバージョンを変更したら、厳密な名前でアセンブリに署名します。fusion が最新バージョンのカスタマイズを読み込むようになります。

 [!NOTE]
> Visual Studio 2017 以降では、アセンブリバージョンでワイルドカードを使用しようとすると、ビルドエラーが発生します。  これは、アセンブリバージョンのワイルドカードによって MSBuild の決定的な機能が無効になるためです。 ワイルドカードをアセンブリのバージョンから削除するか、決定性を無効にするかを指定します。  決定的な機能の詳細については、「[共通の MSBuild プロジェクトのプロパティ](../msbuild/common-msbuild-project-properties.md)」と「[ビルドをカスタマイズ](../msbuild/customize-your-build.md)する」を参照してください。

## <a name="installation-fails-when-the-uri-has-characters-that-arent-us-ascii"></a>URI に us-ascii 以外の文字が含まれていると、インストールが失敗する
 Office ソリューションを HTTP、HTTPS、または FTP のいずれかの場所に発行する場合、US-ASCII ではない Unicode 文字をパスに含めることはできません。 これらの文字を使用すると、セットアップ プログラムで一貫性のない動作が実行されることがあります。 インストール パスには、US-ASCII 文字を使用してください。

## <a name="prompt-to-manually-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>開発用コンピューターにソリューションを発行してインストールすると、手動によるアンインストールを求めるメッセージが表示される
 Office ソリューションをビルドすると、そのビルド バージョンが自動的に登録されます。 開発用コンピューターに同じソリューションを以前に発行およびインストールしていた場合は、次のビルド後、リビルド後、または発行後に、発行されたバージョンとビルドされたバージョンのインストール パスが違うことが [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって検出されます。 "現在他のバージョンがインストールされており、この場所からアップグレードすることはできないため、このカスタマイズをインストールすることはできません。" というエラー メッセージが表示されます。 レジストリ キーは、ソリューションがビルドされるたびに更新されます。 したがって、新しいバージョンを発行、デバッグ、または実行する前に、以前のバージョンをアンインストールする必要があります。

 このメッセージが表示されないようにするには、開発用コンピューターで別のユーザー アカウントを作成して配置をテストします。 または、次回のソリューションの発行、デバッグ、またはリビルドの前に、コンピューター上にインストールされているプログラムの一覧からそのバージョンをアンインストールできます。

## <a name="uncaught-exception-or-method-not-found-error-when-you-install-a-solution"></a>ソリューションをインストールするときにキャッチされていない例外またはメソッドが見つからないエラー
 配置マニフェスト ( *.vsto* ファイル)、office アプリケーション、ドキュメント、またはブックを開いて office ソリューションをインストールすると、次の条件に該当するエラーメッセージが表示される場合があります。

- メソッドが見つからない

- MissingMethodException

- キャッチされない例外

  これらのエラー メッセージが表示されないようにするには、セットアップ プログラムを実行することにより、ソリューションをインストールします。

  セットアップ プログラムを実行せずにソリューションをインストールする場合、インストーラーでは、必須コンポーネントの有無のチェックや、それらのインストールは行われません。 セットアップ プログラムは、正しいバージョンの必須コンポーネントをチェックし、必要に応じて、これらをインストールします。

## <a name="manifest-registry-keys-for-add-ins-change-after-an-installshield-limited-edition-project-is-built"></a>InstallShield 限定エディションプロジェクトがビルドされた後にアドインのマニフェストレジストリキーが変更される
 VSTO アドインセットアッププログラムの一部であるマニフェストレジストリキーは、InstallShield 制限付きエディションプロジェクトをビルドするときに、 *.vsto* から *.dll* に変更されることがあります。

 この問題の発生を防ぐには、InstallShield Limited Edition プロジェクトを別のソリューションで作成するか、レジストリ キー値として VSTO アドイン名が含まれる CompanyName.AddinName を使用します。

## <a name="the-clickonce-installer-for-your-office-solution-doesnt-install-the-primary-interop-assemblies"></a>Office ソリューションの ClickOnce インストーラーでプライマリ相互運用機能アセンブリがインストールされない
 Office ソリューション用に ClickOnce が作成するセットアップ プログラムを実行すると、Office プライマリ相互運用機能アセンブリ (PIA) がまだインストールされていない場合のみ、PIA のインストーラーが実行されます。

 セットアッププログラムで Pia が正しくインストールされない場合は、インストールディレクトリから *o2007pia.msi* という名前のインストーラーファイルを実行して、手動でインストールします。

## <a name="reinstall-office-solutions-causes-an-argument-out-of-range-exception"></a>Office ソリューションを再インストールすると、引数が範囲外であるという例外が発生する
 Office ソリューションを再インストールするときに、 <xref:System.ArgumentOutOfRangeException> 例外が発生し、"指定された引数は、有効な値の範囲内にありません" というエラー メッセージが表示される場合があります。

 インストール場所の URL の大文字と小文字が違っていると、この状況が発生します。 たとえば、このエラーは、初めて Office ソリューションをインストールし、2回目を使用した場合に表示され `http://fabrikam.com/ExcelSolution.vsto` `http://fabrikam.com/excelsolution.vsto` ます。

 このエラー メッセージが表示されないようにするには、Office ソリューションのインストール時に、同じ大文字と小文字の組み合わせを使用します。

## <a name="cant-install-a-clickonce-solution-by-opening-the-deployment-manifest-from-the-web"></a>Web から配置マニフェストを開いて ClickOnce ソリューションをインストールすることはできません
 ユーザーは、Web で配置マニフェストを開くことにより、Office ソリューションをインストールできます。 ただし、インターネットインフォメーションサービス (IIS) の一部のインストールでは、 *.vsto* ファイル名拡張子はブロックされます。 Office ソリューションの配置に使用する前に、IIS で MIME の種類を定義する必要があります。

 IIS 7 で MIME の種類を定義する方法の詳細については、「 [mime の種類を追加する (IIS7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725608(v=ws.10))」を参照してください。

 拡張子を **.vsto** に、MIME の種類を " **application/x-ms-vsto**" に設定します。

## <a name="see-also"></a>関連項目

- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)