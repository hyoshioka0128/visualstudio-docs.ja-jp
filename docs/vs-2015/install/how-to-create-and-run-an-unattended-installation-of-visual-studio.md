---
title: '方法: 無人インストールを作成して実行する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- installing Visual Studio, unattended
- unattended installation, Visual Studio
ms.assetid: 3867b5dc-ed34-4ee2-be32-a42e7e320517
caps.latest.revision: 44
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 26e059d4fdc8eadd422924dd6bbda6f7c945ccfb
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433048"
---
# <a name="how-to-create-and-run-an-unattended-installation-of-visual-studio"></a>方法: Visual Studio の無人インストールを作成して実行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインストール アプリケーションは、DVD などのメディアの代わりに、イントラネット経由での無人インストール (つまり、カスタマイズしたサイレント インストール) として実行できます。 このトピックでは、ネットワーク共有からのこの種のインストールのために [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を準備する方法について説明します。

## <a name="creating-a-network-image"></a>ネットワーク イメージの作成
 最初に、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] メディアのネットワーク イメージを作成します。

#### <a name="to-create-a-network-image"></a>ネットワーク イメージを作成するには

1. サーバー上にフォルダー (<*ドライブ*>:\IDEinstall\\ など) を作成します。

2. [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) からインストーラーをダウンロードした後、*Product*.exe /Layout *Drive*:\IDEinstall\ を実行します

3. ネットワーク上で IDEinstall フォルダーを共有してから、適切なセキュリティ設定を行います。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインストール アプリケーションのネットワーク パスは、\\\\*ServerName*\IDEinstall\\*Product*.exe のようになります。

    > [!NOTE]
    > パスとファイル名の組み合わせが 260 文字を超えると、インストールに失敗する場合があります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のパスの最大長は 221 文字です。  ローカル パス名は 70 文字、ネットワーク パス名は 39 文字を超えないようにしてください。

     また、空白文字を含むフォルダー名をパスに指定した場合も、インストールに失敗する可能性があります (例: "\\\\*ServerName*\IDE install"、\\\\*ServerName*\Visual Studio\\)。

## <a name="deploying-visual-studio-in-unattended-mode"></a>無人モードでの Visual Studio の配置
 無人モードで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を配置するには、AdminDeployment.xml ファイルを変更する必要があります。 これを行うには、`/CreateAdminFile` "*\<ファイルの場所>*" コマンド ライン パラメーターを使用して、最初に AdminDeployment.xml ファイルを作成する必要があります。 次に、このファイルを *Drive*:\IDEinstall\packages ディレクトリに配置した場合は、そのファイルを使用して、Visual Studio 配置をネットワークにプッシュするか、インストール環境にプルすることができます。 AdminDeployment.xml ファイルは、オペレーティング システム、アーキテクチャ、Visual Studio のエディション、またはオペレーティング システムの言語に固有のものではありません。

> [!CAUTION]
> 場合によっては、AdminDeployment.xml ファイルで選択済みとして表示されている項目はインストールされません。 この問題を解決するには、"Selected="yes"" とマークされている項目を AdminDeployment.xml ファイルの **最後** に配置します。
>
> 項目のオプションの依存関係をインストールしない場合は、以下のスクリーン ショットに示されているように、最初に親を選択し、次に親の後ろのオプションの依存関係を選択解除します。
>
> ![AdminDeployment.xml ファイルの末尾にあるインストール項目](../install/media/vs2015-install-endoffileadmindeploy.PNG "vs2015_Install_EndOfFileAdminDeploy")
>
> これを実行する別の方法は、親のオプションの子を単に省略する方法です。つまり、"Selected="no"" の項目を一切含めません。ただし、やはり、"Selected="yes"" の項目はすべて AdminDeployment.xml ファイルの最後に配置する必要があります。

> [!IMPORTANT]
> インストール中に、コンピューターが自動的に 1 回以上再起動する場合があります。 再起動した後は、コンピューターが再起動する前にインストールを行うためにログインしていたのと同じユーザー アカウントを使用して再度ログインする必要があります。 無人インストールを実行する前に必須コンポーネントをインストールしておくと、自動再起動を回避できます。 詳細については、 [Visual Studio Administrator Guide](../install/visual-studio-administrator-guide.md)の「セットアップ中の再起動の回避」セクションを参照してください。

 AdminDeployment ファイル スキーマには、次の要素が含まれています。

|要素|属性|値|説明|
|-------------|---------------|------------|-----------------|
|BundleCustomizations|TargetDir|*パス*|インストール アプリケーションのユーザー インターフェイスでパスをオーバーライドした場合と同じように動作します。 Visual Studio が既にインストールされている場合、この要素は無視されます。|
|BundleCustomizations|NoWeb|はい&#124;既定|この要素の値が yes の場合は、セットアップ中にインストール アプリケーションが Web にアクセスすることはありません。|
|SelectableItemCustomization|非表示|はい&#124;なし|この要素の値が Yes の場合は、カスタマイズ ツリーの選択可能な項目が非表示になります。|
|SelectableItemCustomization|選択済み|はい&#124;なし|カスタマイズ ツリーの選択可能な項目を選択または選択解除します。|
|BundleCustomizations|フィード|パス|ユーザーが使用するフィードの場所。  これ以降のこのコンピューターに対する変更操作では、このフィードが使用されます (既定では "Default") 。|
|BundleCustomizations|SuppressRefreshPrompt|はい&#124;既定|使用可能な新しいバージョンがある場合に、ユーザーにセットアップを更新するように要求しなくなります。|
|BundleCustomizations|NoRefresh|はい&#124;既定|使用可能な新しいバージョンがある場合に、セットアップを更新しません。|
|BundleCustomizations|NoCacheOnlyMode|はい&#124;既定|パッケージ キャッシュの事前設定を防ぎます。|

> [!WARNING]
> インストール アプリケーションでは、選択可能な項目が非表示になっている場合でも、その Selected の状態が反映されます。 たとえば、ある選択可能な項目を常にインストールする場合は、その項目を非表示で選択済みとしてマークできます。

#### <a name="to-create-an-unattended-installation-of-visual-studio"></a>Visual Studio の無人インストールを作成するには

1. *Drive*:\IDEinstall\AdminDeployment.xml ファイルで、次の例に示すように、BundleCustomizations 要素の NoWeb の属性の値を "default" から "yes" に変更します。

     `<BundleCustomizations TargetDir="default" NoWeb="default"/>` を `<BundleCustomizations TargetDir="default" NoWeb="yes"/>` に変更します

2. 必要に応じてオプションのコンポーネントの SelectableItemCustomization 属性を変更し、ファイルを保存します。

## <a name="running-unattended-setup"></a>無人セットアップの実行
 無人セットアップを実行するには、クライアント コンピューターで Visual Studio のインストール アプリケーションを自動的に実行するか、定義した設定を使用してユーザーが自分でアプリケーションを実行できるようにします。

#### <a name="to-run-an-unattended-installation-on-a-client-computer"></a>クライアント コンピューターで無人インストールを実行するには

- **[スタート]** メニューを開き、**[実行]** を選択してから、「\\\\*ServerName*\IDEinstall\vs_*Product*.exe /adminfile *PathOfTheAdmindeployment.xmlFile*<em>AdditionalParametersAsNeeded</em>」と入力します

   たとえば、`\\server1\IDEinstall\vs_enterprise.exe /adminfile \\server1\ IDEinstall\AdminDeployment.xml /quiet /norestart` というコマンド ラインを指定できます。

#### <a name="to-enable-clients-to-manually-install-visual-studio-with-pre-defined-settings"></a>クライアントで、定義済みの設定を使用して Visual Studio を手動でインストールできるようにするには

1. カスタマイズした AdminDeployment.xml ファイルを読み取り専用のネットワーク共有 (例: \\\\*ServerName*\IDEinstall\packages\AdminDeployment.xml) にコピーします。

2. ユーザーがその共有からインストールできるようにします。

## <a name="maintaining-an-installation"></a>インストールの保守
 **コントロール パネル** を開き、インストール アプリケーションを再実行すると、Visual Studio の機能の変更、プログラミング言語のアンインストール、および Visual Studio の修復またはアンインストールを実行できます。

> [!NOTE]
> メンテナンス モードを使用するには、ローカル コンピューターの管理者の資格情報を持っている必要があります。

#### <a name="to-maintain-an-installation-on-a-client-computer"></a>クライアント コンピューターでインストールの保守を行うには

- **コントロール パネル**を開き、 **[プログラムと機能]** を選択します。

- [ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]] を選択し、 **[変更]** を選択します。

#### <a name="to-change-admindeployment-settings-on-a-client-computer-after-visual-studio-has-been-installed"></a>Visual Studio をインストールした後にクライアント コンピューターで AdminDeployment の設定を変更するには

1. 必要に応じて、AdminDeployment.xml を更新します。

2. **[スタート]** メニューを開き、 **[ファイル名を指定して実行]** を選択します。

3. 次のテキストを入力します: \\\\*ServerName*\IDEinstall\vs_*Product*.exe /AdminFile PathToAdmindeployment.xml File

    AdditionalParametersAsNeeded

    たとえば、`\\server1\IDEinstall\vs_enterprise.exe /adminfile \\server1\IDEinstall\AdminDeployment.xml /quiet /norestart` というコマンド ラインを指定できます。

   修復は、Visual Studio をインストールした後の既定のパラメーターです。 更新した /AdminFile を使用して Visual Studio を修復すると、現在の管理者モード配置設定が、更新した AdminDeployment.xml ファイルにより呼び出される設定でオーバーライドされます。

## <a name="updating-an-installation"></a>インストールの更新
 Microsoft により、Visual Studio 2015 の更新プログラムがいくつかリリースされています。 このセクションでは、更新プログラムを含むよう Visual Studio 2015 の無人インストール イメージを更新する方法について説明します。

#### <a name="to-update-an-unattended-installation-of-visual-studio"></a>Visual Studio の無人インストールを更新するには

1. 既存のネットワーク イメージから Product.exe ファイルを探して右クリックした後、**[プロパティ]** をクリックします。

2. **[詳細]** タブをクリックした後、**[製品バージョン]** プロパティをメモしておきます。

    ![Visual Studio の無人インストールにおける [プロパティ] ダイアログ ボックスの例](../install/media/unattended-install-properties-dialog-box.PNG "無人インストール - [プロパティ] ダイアログ ボックス")

3. ###### <a name="if-the-product-version-is-140247200-or-140247201-follow-these-steps"></a>製品のバージョンが 14.0.24720.0 または 14.0.24720.1 の場合は、次の手順に従います。
   1. インターネットにアクセスできるコンピューター上で *Product.exe* /Layout *Drive:* \IDEinstall を実行します。 (たとえば、`vs_enterprise.exe /Layout d:\IDEinstall` を実行します。)

   2. /Layout が完了したら、新しいイメージを新しい場所にコピーします。

   3. AdminDeployment.xml ファイルを作成して変更します。 これを行うには、`/CreateAdminFile`"*\<ファイルの場所>*" コマンド ライン パラメーターを使います。 (詳細については、この記事の「無人モードでの Visual Studio の配置」セクションをご覧ください。)

   4. クライアント コンピューター上で次のコマンドを実行して、前にインストールした Visual Studio のコピーを更新します: "\\\\*server1*\IDEinstall_Updated_1\\*Product.exe* /adminfile \\\server1\ IDEinstall_Updated_1\AdminDeployment.xml /quiet /norestart"。

        たとえば、`\\server1\IDEinstall_Updated_1\vs_enterprise.exe /adminfile \\server1\IDEinstall_Updated_1\AdminDeployment.xml /quiet /norestart` を実行します
5. ###### <a name="for-other-product-version-values-follow-these-steps"></a>その他の製品バージョンの値については、次の手順に従います。
   1. インターネットにアクセスできるコンピューター上で *Product.exe* /Layout *Drive:* \IDEinstall を実行します。 (たとえば、`vs-enterprise.exe /Layout d:\IDEinstall` を実行します。)

   2. /Layout が完了したら、新しいイメージを新しい場所にコピーします。 (または、代わりに既存のネットワーク イメージを上書きすることができます。)

   3. AdminDeployment.xml ファイルを作成した後、変更します。 これを行うには、`/CreateAdminFile`"*\<ファイルの場所>*" コマンド ライン パラメーターを使います。 (詳細については、この記事の「無人モードでの Visual Studio の配置」セクションをご覧ください。)

   4. イメージを新しい場所にコピーする場合、クライアント コンピューター上で次のコマンドを実行して、前にインストールした Visual Studio のコピーを更新する必要があります: "\\\\*server1*\IDEinstall_Updated_1\\*Product.exe* /adminfile \\\server1\ IDEinstall_Updated_1\AdminDeployment.xml /quiet /norestart"。

        たとえば、`\\server1\IDEinstall_Updated_1\vs_enterprise.exe /adminfile \\server1\IDEinstall_Updated_1\AdminDeployment.xml /quiet /norestart` を実行します

   5. 既存のネットワーク イメージをオーバーライドする場合は、前の手順に記載されているコマンドを実行するか、または以下の操作を行うことができます。
       1. **コントロール パネル**を開き、 **[プログラムと機能]** を選択します。

       2. **[Visual Studio]** を選択してから、**[変更]** を選択します。

       3. Visual Studio がメンテナンス モードで起動したら、**[変更]** をクリックします。

       4. 最新の更新プログラムが [機能] ページに表示されます。 インストールしたい他の機能を選択し、**[次へ]** をクリックしてから、**[更新]** をクリックして更新プログラムと新機能の両方をインストールします。

## <a name="registering-the-product"></a>製品の登録
 インストールが完了したら、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内から [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]のコピーを登録できます。

#### <a name="to-register"></a>登録するには

1. **[ヘルプ]** メニューを開き、 **[製品の登録]** をクリックします。

2. プロダクト キーを入力します。

     (詳細については、「[How to: Locate the Visual Studio Product Key (方法: Visual Studio プロダクト キーを検索する)](../install/how-to-locate-the-visual-studio-product-key.md)」と「[How to: Automatically apply product keys when deploying Visual Studio (方法: Visual Studio の展開時にプロダクト キーを自動的に適用する)](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md)」トピックをご覧ください。)

## <a name="see-also"></a>関連項目
 [Visual Studio のインストール](../install/install-visual-studio-2015.md)
