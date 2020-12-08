---
title: Windows インストーラーを使用した VSTO ソリューションの配置
description: Visual Studio インストーラープロジェクトを使用して、Microsoft Visual Studio Tools for Office (VSTO) アドインまたはドキュメントレベルのソリューションを配置する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/18/2010
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, setup project
- Office development in Visual Studio, MSI
- deploying applications [Office development in Visual Studio], setup project
- deploying applications [Office development in Visual Studio], MSI
- ClickOnce deployment [Office development in Visual Studio], MSI
- publishing Office solutions [Office development in Visual Studio], setup project
- Office applications [Office development in Visual Studio], MSI
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e49705c99801cd6e09f4bf6d9be3c411cc2c53e3
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846546"
---
# <a name="deploying-a-vsto-solution-using-windows-installer"></a>Windows インストーラーを使用した VSTO ソリューションの配置

## <a name="summary"></a>まとめ

Visual Studio インストーラープロジェクトを使用して、Microsoft Visual Studio Tools for Office (VSTO) アドインまたはドキュメントレベルのソリューションを配置する方法について説明します。

Wouter van V氏、Code 弁護士

Ted のシャード son グループ

この記事は、Microsoft によって、元の作成者からのアクセス許可を使用して更新されました。

**適用対象:** Visual Studio Tools for Office、Microsoft Office、Microsoft Visual Studio。

## <a name="overview"></a>概要

VSTO ソリューションを開発し、Windows インストーラーパッケージを使用してソリューションを配置することができます。 ここでは、簡単な Office アドインを展開する手順について説明します。

## <a name="deployment-methods"></a>配置方法

ClickOnce を使用すると、アドインとソリューションのセットアップを簡単に作成できます。 ただし、コンピューターレベルのアドインなどの管理者特権を必要とするアドインをインストールすることはできません。

管理特権を必要とするアドインは Windows インストーラーを使用してインストールできますが、セットアップを作成するにはより多くの労力が必要です。

ClickOnce を使用して VSTO ソリューションを配置する方法の概要については、「 [clickonce を使用した Office ソリューションの配置](deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="deploying-office-solutions-that-target-the-vsto-runtime"></a>VSTO ランタイムを対象とする Office ソリューションの配置

ClickOnce と Windows インストーラーパッケージは、Office ソリューションをインストールするときに、同じ基本的なタスクを実行する必要があります。

1. ユーザーのコンピューターに必須コンポーネントをインストールします。
2. ソリューションの特定のコンポーネントを配置します。
3. アドインの場合は、レジストリエントリを作成します。
4. ソリューションを信頼して実行できるようにします。

### <a name="required-prerequisite-components-on-the-target-computer"></a>ターゲットコンピューターに必要な前提条件コンポーネント

VSTO ソリューションを実行するためにコンピューターにインストールする必要があるソフトウェアの一覧を次に示します。

- Microsoft Office 2010 以降。
- Microsoft .NET Framework 4 以降。
- Microsoft Visual Studio 2010 Tools for Office Runtime
  ランタイムには、アドインとドキュメントレベルのソリューションを管理する環境が用意されています。 ランタイムのバージョンには Microsoft Office が付属していますが、アドインを使用して特定のバージョンを再配布することもできます。
- 埋め込まれた相互運用機能型を使用していない場合、Microsoft Office のプライマリ相互運用機能アセンブリ。
- プロジェクトによって参照されるすべてのユーティリティアセンブリ。

### <a name="specific-components-for-the-solution"></a>ソリューションの特定のコンポーネント

インストーラーパッケージは、次のコンポーネントをユーザーのコンピューターにインストールする必要があります。

- ドキュメントレベルのソリューションを作成する場合は、Microsoft Office ドキュメント。
- カスタマイズアセンブリとそれに必要なすべてのアセンブリ。
- 構成ファイルなどの追加のコンポーネント。
- アプリケーションマニフェスト (.manifest)。
- 配置マニフェスト (.vsto)。

### <a name="registry-entries-for-add-ins"></a>アドインのレジストリエントリ

Microsoft Office は、レジストリエントリを使用してアドインを検索して読み込みます。これらのレジストリエントリは、デプロイプロセスの一部として作成する必要があります。 これらのレジストリエントリの詳細については、「 [VSTO アドインのレジストリエントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

カスタムフォーム領域を表示する Outlook アドインには、フォーム領域を識別できるようにする追加のレジストリエントリが必要です。 レジストリエントリの詳細については、「 [Outlook フォーム領域のレジストリエントリ](registry-entries-for-vsto-add-ins.md#OutlookEntries)」を参照してください。

ドキュメントレベルのソリューションでは、レジストリエントリは必要ありません。 代わりに、ドキュメント内のプロパティを使用して、カスタマイズを見つけます。 これらのプロパティの詳細については、「 [カスタムドキュメントプロパティの概要](custom-document-properties-overview.md)」を参照してください。

### <a name="trusting-the-vsto-solution"></a>VSTO ソリューションの信頼

カスタマイズを実行するには、ソリューションがコンピューターによって信頼されている必要があります。 アドインは、証明書を使用してマニフェストに署名するか、信頼の一覧との信頼関係を作成するか、コンピューター上の信頼できる場所にインストールすることによって信頼できます。

署名用の証明書を取得する方法の詳細については、「 [ClickOnce 配置と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。 ソリューションの信頼の詳細については、「信頼の [リストを使用した Office ソリューションの信頼](trusting-office-solutions-by-using-inclusion-lists.md)」を参照してください。 Windows インストーラーファイルにカスタムアクションと共に、信頼リストエントリを追加できます。 信頼の一覧を有効にする方法の詳細については、「 [方法: 信頼のリストのセキュリティを構成する](how-to-configure-inclusion-list-security.md)」を参照してください。

どちらのオプションも使用しない場合、ユーザーに対して信頼プロンプトが表示され、ソリューションを信頼するかどうかを判断できます。

ドキュメントレベルのソリューションに関連するセキュリティの詳細については、「 [ドキュメントへの信頼の付与](granting-trust-to-documents.md)」を参照してください。

## <a name="creating-a-basic-installer"></a>基本的なインストーラーを作成する

セットアップおよび配置プロジェクトテンプレートは、ダウンロード可能な [Microsoft Visual Studio Installer プロジェクト](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects) の拡張機能に含まれています。

Office ソリューションのインストーラーを作成するには、次のタスクを実行する必要があります。

- 配置される Office ソリューションのコンポーネントを追加します。
- アプリケーションレベルのアドインの場合は、レジストリキーを構成します。
- エンドユーザーのコンピューターにインストールできるように、前提条件コンポーネントを構成します。
- 起動条件を構成して、必要な前提条件コンポーネントが使用可能であることを確認します。 必要なすべての前提条件がインストールされていない場合は、起動条件を使用してインストールをブロックできます。

最初の手順では、セットアッププロジェクトを作成します。

### <a name="to-create-the-addin-setup-project"></a>AddIn セットアッププロジェクトを作成するには

1. 配置する Office アドインプロジェクトを開きます。 この例では、ExcelAddIn と呼ばれる Excel アドインを使用しています。
2. Office プロジェクトを開いた状態で、[ **ファイル** ] メニューの [ **追加** ] を展開し、[ **新しいプロジェクト** ] をクリックして新しいプロジェクトを追加します。
::: moniker range="=vs-2017"
3. [**新しいプロジェクトの追加**] ダイアログで、[プロジェクトの **種類**] ペインの [**その他のプロジェクトの種類**] を展開し、[**セットアップと配置**] を展開して [ **Visual Studio インストーラー**] を選択します。
4. [**テンプレート**] ペインで、[ **Visual Studio にインストールさ** れたテンプレート] グループから [**セットアッププロジェクト**] を選択します。
::: moniker-end
::: moniker range="=vs-2019"
3. [ **新しいプロジェクトの追加** ] ダイアログで、[ **セットアッププロジェクト** ] テンプレートを選択します。
4. **[次へ]** をクリックします。
::: moniker-end

5. [ **名前** ] ボックスに「 **officeaddinsetup**」と入力します。
::: moniker range="=vs-2017"
6. [ **開く** ] をクリックして、新しいセットアッププロジェクトを作成します。
::: moniker-end
::: moniker range="=vs-2019"
6. [ **作成** ] をクリックして、新しいセットアッププロジェクトを作成します。
::: moniker-end

Visual Studio によって、新しいセットアッププロジェクトのファイルシステムエクスプローラーが開きます。 ファイルシステムエクスプローラーを使用すると、セットアッププロジェクトにファイルを追加できます。

   ![セットアッププロジェクトのファイルシステムエクスプローラーのスクリーンショット](media/setup-project-figure-1.png)

   **図 1: セットアッププロジェクトのファイルシステムエクスプローラー**

セットアッププロジェクトでは、ExcelAddIn を配置する必要があります。 このタスクのセットアッププロジェクトは、ExcelAddIn プロジェクトの出力をセットアッププロジェクトに追加することによって構成できます。

### <a name="to-add-the-exceladdin-project-output"></a>ExcelAddIn プロジェクトの出力を追加するには

1. **ソリューションエクスプローラー** で、[ **officeaddinsetup**] を右クリックし、[**追加**]、[**プロジェクト出力**] の順にクリックします。
2. [ **プロジェクト出力グループの追加** ] ダイアログで、[プロジェクト] ボックスの一覧から **exceladdin** を選択し、[ **プライマリ出力**] を選択します。
3. [ **OK]** をクリックして、プロジェクトの出力をセットアッププロジェクトに追加します。

    ![セットアッププロジェクトの [プロジェクト出力グループの追加] ダイアログのスクリーンショット](media/setup-project-figure-2.png)

    **図 2: セットアッププロジェクトの [プロジェクト出力グループの追加] ダイアログ**

セットアッププロジェクトでは、配置マニフェストとアプリケーションマニフェストを配置する必要があります。 これらの2つのファイルを、ExcelAddIn プロジェクトの出力フォルダーにあるスタンドアロンファイルとしてセットアッププロジェクトに追加します。

### <a name="to-add-the-deployment-and-application-manifests"></a>配置マニフェストとアプリケーションマニフェストを追加するには

1. **ソリューションエクスプローラー** で、[ **officeaddinsetup**] を右クリックし、[**追加**] をクリックして、[**ファイル**] をクリックします。
2. [ **ファイルの追加** ] ダイアログボックスで、 **exceladdin** 出力ディレクトリに移動します。 通常、出力ディレクトリは、選択したビルド構成に応じて、プロジェクトルートディレクトリの **bin \\ リリース** サブフォルダーになります。
3. **Exceladdin** ファイルと **ExcelAddIn.dll マニフェスト** ファイルを選択し、[**開く**] をクリックして、これらの2つのファイルをセットアッププロジェクトに追加します。

    ![ソリューションエクスプローラーのアプリケーションマニフェストと配置マニフェストのスクリーンショット](media/setup-project-figure-3.jpg)

    **図 3: ソリューションエクスプローラーでのアドインのアプリケーションマニフェストと配置マニフェスト**

ExcelAddIn の参照には、ExcelAddIn に必要なすべてのコンポーネントが含まれています。 これらのコンポーネントを正しく登録できるようにするには、前提条件のパッケージを使用して除外および展開する必要があります。 また、インストールを開始する前に、ソフトウェアライセンス条項を表示して同意する必要があります。

### <a name="to-exclude-the-exceladdin-project-dependencies"></a>ExcelAddIn プロジェクトの依存関係を除外するには

1. **ソリューションエクスプローラー** の [ **officeaddinsetup** ] ノードで、[**検出された依存関係**] 項目の下にある [すべての依存関係項目] を選択します。ただし、 **Microsoft .NET Framework** または **\*.Utilities.dll** で終わるアセンブリは除きます。 ユーティリティアセンブリは、アプリケーションと共に配置することを意図しています。
2. グループを右クリックし、[ **プロパティ**] を選択します。
3. [ **プロパティ** ] ウィンドウで、[ **除外** ] プロパティを [ **True** ] に変更して、依存アセンブリをセットアッププロジェクトから除外します。 ユーティリティアセンブリを除外しないようにしてください。

    ![除外する依存関係を示すソリューションエクスプローラーのスクリーンショット](media/setup-project-figure-4.jpg)

    **図 4: 依存関係を除外する**

ブートストラップとも呼ばれるセットアッププログラムを追加することによって、前提条件コンポーネントをインストールするように Windows インストーラーパッケージを構成できます。 このセットアッププログラムでは、ブートストラップと呼ばれるプロセスである前提条件コンポーネントをインストールできます。

**Exceladdin** の場合、アドインを正しく実行するには、これらの前提条件をインストールする必要があります。

- Office ソリューションが対象とする Microsoft .NET Framework のバージョン。
- Microsoft Visual Studio 2010 Tools for Office Runtime。

依存コンポーネントを前提条件として構成するには

1. **ソリューションエクスプローラー** で、 **officeaddinsetup** プロジェクトを右クリックし、[**プロパティ**] を選択します。
2. [ **Officeaddinsetup プロパティページ** ] ダイアログボックスが表示されます。
3. [ **必須コンポーネント** ] ボタンをクリックします。
4. [必須コンポーネント] ダイアログボックスで、適切なバージョンの .NET Framework と Microsoft Visual Studio Tools for Office Runtime を選択します。

    ![[必須コンポーネント] ダイアログボックスのスクリーンショット](media/setup-project-figure-5.png)

    **図 5: [必須コンポーネント] ダイアログボックス**

    > [!NOTE]
    >Visual Studio セットアッププロジェクトで構成されている前提条件パッケージのいくつかは、選択したビルド構成に依存しています。 使用する各ビルド構成に対して適切な前提条件コンポーネントを選択する必要があります。

Microsoft Office は、レジストリキーを使用してアドインを検索します。 HKEY CURRENT user hive 内のキーを使用して、 \_ \_ 個々のユーザーにアドインが登録されます。 HKEY LOCAL machine ハイブの下にあるキーを使用して、 \_ \_ コンピューターのすべてのユーザーにアドインが登録されます。 レジストリキーの詳細については、「 [VSTO アドインのレジストリエントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

### <a name="to-configure-the-registry"></a>レジストリを構成するには

1. **ソリューションエクスプローラー** で、[ **officeaddinsetup**] を右クリックします。
2. [ **表示**] を展開します。
3. [ **レジストリ** ] をクリックして、[レジストリエディター] ウィンドウを開きます。
4. **レジストリ (OfficeAddInSetup)** エディターで、[ **HKEY \_ LOCAL \_ MACHINE** ]、[ **Software**] の順に展開します。
5. **\[ 製造元 \]** を削除しますか? キーは **HKEY \_ LOCAL \_ MACHINE \\ Software** の下にあります。
6. [ **HKEY \_ CURRENT \_ USER** ]、[ **Software**] の順に展開します。
7. **HKEY \_ CURRENT \_ USER \\ Software** で見つかった **\[ 製造元 \]** キーを削除します。
8. アドインのインストール用のレジストリキーを追加するには、 **ユーザーまたはコンピューターの Hive** キーを右クリックし、[ **新しいキー**] を選択します。 新しいキーの名前には、テキスト **ソフトウェア** を使用します。 新しく作成した **ソフトウェア** キーを右クリックし、「 **Microsoft**」というテキストを含む新しいキーを作成します。
9. 同様のプロセスを使用して、アドインの登録に必要なキー階層全体を作成します。

    **ユーザー/コンピューターの Hive \\ ソフトウェア \\ Microsoft \\ Office \\ Excel \\ Addins \\ の**

    会社名は、多くの場合、一意のアドイン名のプレフィックスとして使用されます。

10. **の** キーを右クリックし、[**新規作成**] をクリックして、[**文字列値**] をクリックします。 名前に「 **Description** 」というテキストを使用します。
11. このステップでは、次の3つの値を追加します。
    - **文字列** 型の **FriendlyName**
    - **LoadBehavior** 型の **DWORD**
    - **文字列** 型の **マニフェスト**

12. レジストリエディターで [ **説明** ] の値を右クリックし、[ **プロパティウィンドウ**] をクリックします。 [ **プロパティ] ウィンドウ** で、[値] プロパティに「 **Excel Demo AddIn** 」と入力します。
13. レジストリエディターで **FriendlyName** キーを選択します。 [ **プロパティ] ウィンドウ** で、[ **値** ] プロパティを [ **Excel Demo AddIn**] に変更します。
14. レジストリエディターで **LoadBehavior** キーを選択します。 [ **プロパティ] ウィンドウ** で、[ **値** ] プロパティを3に変更し **ます。** LoadBehavior の値3は、ホストアプリケーションの起動時にアドインを読み込む必要があることを示します。 読み込み動作の詳細については、「 [VSTO アドインのレジストリエントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

15. レジストリエディターで **マニフェスト** キーを選択します。 [**プロパティ] ウィンドウ** で、 **Value** プロパティを **file:///[TARGETDIR] exceladdin. vsto | vstolocal** に変更します。

    ![レジストリエディターのスクリーンショット](media/setup-project-figure-6.png)

    **図 6: レジストリキーの設定**

      VSTO ランタイムは、このレジストリキーを使用して配置マニフェストを検索します。 [TARGETDIR] マクロは、アドインがインストールされているフォルダーに置き換えられます。 マクロには末尾の \ 文字が含まれるため、配置マニフェストのファイル名は、\ 文字を含まない ExcelAddIn にする必要があります。
      **Vstolocal** 後置は、アドインが ClickOnce キャッシュではなくこの場所から読み込む必要があることを VSTO ランタイムに通知します。 この後置を削除すると、ランタイムによってカスタマイズが ClickOnce キャッシュにコピーされます。

   >[!WARNING]
   >Visual Studio では、レジストリエディターに細心の注意を払ってください。 たとえば、間違ったキーに対して DeleteAtUninstall を誤って設定した場合、レジストリのアクティブな部分を削除して、ユーザーのコンピューターが不整合な状態になるか、さらに悪化した状態になる可能性があります。

64ビット版の Office では、64ビットのレジストリハイブを使用してアドインを検索します。64ビットレジストリハイブでアドインを登録するには、セットアッププロジェクトのターゲットプラットフォームが64ビットのみに設定されている必要があります。

1. ソリューションエクスプローラーで、 **Officeaddinsetup** プロジェクトを選択します。
2. [ **プロパティ** ] ウィンドウにアクセスし、 **TargetPlatform** プロパティを **x64** に設定します。

32ビット版と64ビット版の両方の Office 用アドインをインストールするには、2つの個別の MSI パッケージを作成する必要があります。 1つは32ビット用、もう1つは64ビット用です。

  ![64ビットの Office でアドインを登録するためのターゲットプラットフォームを示す [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-7.jpg)

  **図 7:64 ビットの Office を使用してアドインを登録するためのターゲットプラットフォーム**

MSI パッケージを使用してアドインまたはソリューションをインストールする場合、必要な前提条件をインストールしないとインストールされることがあります。 必須コンポーネントがインストールされていない場合、MSI で起動条件を使用して、アドインのインストールをブロックできます。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime"></a>VSTO ランタイムを検出する起動条件の構成

1. **ソリューションエクスプローラー** で、[ **officeaddinsetup**] を右クリックします。
2. [ **表示**] を展開します。
3. [ **起動条件**] をクリックします。
4. [ **起動条件 (OfficeAddInSetup)** エディター] で、[ **対象コンピューター] の [要件**] を右クリックし、[ **レジストリ起動条件の追加**] をクリックします。 この検索条件では、レジストリで VSTO ランタイムによってインストールされたキーを検索できます。 キーの値は、名前付きプロパティを使用して、インストーラーのさまざまな部分で使用できます。 起動条件では、検索条件で定義されたプロパティを使用して、特定の値を確認します。
5. [ **起動条件 (OfficeAddInSetup)** ] エディターで、[ **search for RegistryEntry1** ] 検索条件を選択し、条件を右クリックして、[ **プロパティウィンドウ**] を選択します。

6. **[プロパティ]** ウィンドウで、次のプロパティを設定します。
   1. **VSTO 2010 Runtime を検索** するには、 **(Name)** の値を設定します。
   2. **プロパティ** の値を **Vstoruntimeredist** に変更します。
   3. **RegKey** の値を **SOFTWARE \\ Microsoft \\ VSTO Runtime Setup \\ v4R** に設定します。
   4. **ルート** プロパティを **Vsdrrhklm** に設定したままにします。
   5. **Value** プロパティを **Version** に変更します。

7. [ **起動条件 (OfficeAddInSetup)** エディター] で、 **Condition1** launch 条件を選択し、条件を右クリックして、[ **プロパティウィンドウ**] を選択します。
8. [プロパティ] ウィンドウで、次のプロパティを設定します。
   1. **(名前)** を設定し **て、VSTO 2010 Runtime の可用性を確認** します。
   2. **条件** の値を **Vstoruntimeredist \> = "10.0.30319"** に変更します。
   3. **InstallURL** プロパティを空白のままにします。
   4. **メッセージ** を **Visual Studio 2010 Tools for Office Runtime がインストールされていないことを設定します。Setup.exe を実行してアドインをインストールしてください**。

        ![[ランタイムの可用性の確認] 起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-8.jpg)

        **図 8: [ランタイムの可用性を確認する] 起動条件のプロパティウィンドウ**

 上記の起動条件は、ブートストラップパッケージによってインストールされるときに VSTO ランタイムが存在するかどうかを明示的に確認します。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime-installed-by-office"></a>Office によってインストールされた VSTO ランタイムを検出する起動条件の構成

1. [ **起動条件 (OfficeAddInSetup)** エディター] で、[ **検索対象コンピューター**] を右クリックし、[ **レジストリ検索の追加**] をクリックします。
2. 検索条件として **RegistryEntry1** 検索条件を選択し、条件を右クリックして、[ **プロパティウィンドウ**] を選択します。
3. **[プロパティ]** ウィンドウで、次のプロパティを設定します。
    1. **OFFICE VSTO Runtime を検索** するには、 **(Name)** の値を設定します。
    2. **プロパティ** の値を、[に変更 **します。**
    3. **RegKey** の値を「 **SOFTWARE \\ Microsoft \\ VSTO Runtime Setup \\ v4**」に設定します。
    4. **ルート** プロパティを **Vsdrrhklm** に設定したままにします。
    5. **Value** プロパティを **Version** に変更します。

4. [ **起動条件 (OfficeAddInSetup)** エディター] で、前に定義した [ **VSTO 2010 ランタイムの可用性** 起動条件を確認する] を選択し、条件を右クリックして、[ **プロパティウィンドウ**] を選択します。

5. **Condition** プロパティの値を **Vstoruntimeredist \> = "10.0.30319" または \> "10.0.21022"** に変更します。 バージョン番号は、アドインで必要とされるランタイムのバージョンによって異なる可能性があります。

    ![起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-9.jpg)
  
    **図 9: Redist または Office 起動条件を使用してランタイムの可用性を確認するためのプロパティウィンドウ**

アドインが .NET Framework 4 以降を対象とする場合は、参照されるプライマリ相互運用機能アセンブリ (PIA) 内の型を VSTO アセンブリに埋め込むことができます。

次の手順を実行して、アドインに相互運用型が埋め込まれるかどうかを確認するには、次の手順を実行します。

1. ソリューションエクスプローラーの [参照] ノードを展開します。
2. PIA 参照の1つを選択します (たとえば、 **Office**)。
3. F4 キーを押すか、アセンブリのショートカットメニューから [プロパティ] を選択して、[プロパティ] ウィンドウを表示します。
4. [ **相互運用機能型の埋め込み** プロパティの値を確認します。

値が **True** に設定されている場合は、型が埋め込まれています。「」に進んで、「 [**セットアッププロジェクトのビルド**](#to-build-the-setup-project) 」セクションを参照してください。

詳細については、「[型の等価性と埋め込み相互運用機能型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)」を参照してください。

### <a name="to-configure-launch-conditions-to-detect-that-for-office-pias"></a>Office Pia で検出する起動条件を構成するには

1. [ **起動条件 (OfficeAddInSetup)** エディター] で、[ **対象コンピューター] の [要件**] を右クリックし、 **[起動条件の Windows インストーラー追加] をクリック** します。 この起動条件は、特定のコンポーネント ID を検索して、Office PIA を検索します。
2. [ **Component1 の検索** ] を右クリックし、[ **プロパティウィンドウ** ] をクリックして起動条件のプロパティを表示します。
3. [ **プロパティ] ウィンドウ** で、次のプロパティを設定します。

    1. **(Name)** プロパティの値を、 **Office 共有 PIA を検索** するように変更します。
    2. **ComponentID** の値を、使用している Office コンポーネントのコンポーネント Id に変更します。 次の表に、コンポーネント Id の一覧を示します (例 **{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}**)。
    3. **プロパティ** プロパティの値を **hassharedpia** に変更します。

4. **起動条件 (OfficeAddInSetup)** エディターで、[ **Condition1** ] を右クリックし、[**プロパティウィンドウ**] をクリックして起動条件のプロパティを表示します。

5. **Condition1** の次のプロパティを変更します。

    1. **Office 共有 PIA の可用性を確認** するには、 **(名前)** を変更します。
    2. **条件** を **hassharedpia** に変更します。
    3. **InstallUrl** を空白のままにします。
    4. Excel との対話に必要なコンポーネントに **メッセージ** を変更する **ことはできません。setup.exeを実行してください**。

    ![Office 共有 PIA の起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-10.jpg)
  
    **図 10: Office 共有 PIA の起動条件のプロパティウィンドウ**

### <a name="component-ids-of-the-primary-interop-assemblies-for-microsoft-office"></a>Microsoft Office のプライマリ相互運用機能アセンブリのコンポーネント Id

|プライマリ相互運用機能アセンブリ|Office 2010|Office 2013|Office 2013 (64 ビット)|Office 2016|Office 2016 (64 ビット)|
|------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|
|Excel|{EA7564AC-C67D-4868-BE5C-26E4FC2223FF}|{C8A65ABE-3270-4FD7-B854-50C8082C8F39}|{E3BD1151-B9CA-4D45-A77E-51A6E0ED322A}|C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|{C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|
|InfoPath|{4153F732D67047 E44-8AB7-500F2B576BDA}|{0F825A16-25B2-4771-A497-FC8AF3B355D8}|{C5BBD36E-B320-47EF-A512-556B99CB7E41}|-|-|
|Outlook|{1D844339-3DAE-413E-BC13-62D6A52816B2}|{F9F828D5-9F0B-46F9-9E3E-9C59F3C5E136}|{7824A03F-28CC-4371-BC54-93D15EFC1E7F}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|
|PowerPoint|{EECBA6B8-3A62-44AD-99EB-8666265466F9}|{813139AD-6DAB-4DDD-8C6D-0CA30D073B41}|{05758318-BCFD-4288-AD8D-8118584 1C235}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|
|Visio|{3EA123B5-6316-452E-9D51-A489E06E2347}|{C1713368-12A8-41F1-ACA1-934B01AD6EEB}|{2CC0B221-22D2-4C15-A9FB-DE818E51AF75}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|
|Word|{8B74A499-37F8-4DEA-B5A0-D72FC501CEFA}|{9FE736B7-B1EE-410C-8D07-082891C3DAC8}|{13C07AF5-B20647 A48(BB5B8022333E3CA})|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|
|Microsoft Forms 2.0|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{A5A30117-2D2A-4C5C-B3C8-8897AC32C2AC}|-|-|
|Microsoft Graph|{011B9112-EBB1-4A6C-86CB-C2FDC9EA7B0E}|{52DA4B37-B8EB-4B7F-89C1-824654CE4C70}|{24706F33-F0CE-4EB4-BC91-9E935394F510}|-|-|
|スマート タグ|{7の自動 (C98C98) EF47 47 F0405 A227-FE33650BF954}|{487A7921-EB3A-4262-BB5B-A5736B732486}|{74EFC1F9 ~ 747 D-4867-B951-EFCF29F51AF7}|-|-|
|Office 共有|{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}|{6A174BDB-0049-4D1C-86EF-3114CB0C4C4E}|{76601EBB-44A7-49EE-8DE3-7B7B9D7EBB05}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|
|プロジェクト|{957A4EC0-E67B-4E86-A383-6AF7270B216A}|{1C50E422-24FA-44A9-A120-E88280C8C341}|{706D7F44-8231-489D-9B25-3025ADE9F114}|{107BCD9A-F1DC-4004-A444-33706FC10058}|{107BCD9A-F1DC-4004-A444-33706FC10058}|

  ![最終的な起動条件のスクリーンショット](media/setup-project-figure-11.jpg)

  **図 11: 最終的な起動条件**

ExcelAddIn インストールの起動条件をさらに絞り込むことができます。 たとえば、実際の対象 Office アプリケーションがインストールされているかどうかを確認すると便利な場合があります。

### <a name="to-build-the-setup-project"></a>セットアッププロジェクトをビルドするには

1. **ソリューションエクスプローラー** で、 **officeaddinsetup** プロジェクトを右クリックし、[**ビルド**] をクリックします。
2. **エクスプローラー** を使用して、 **officeaddinsetup** プロジェクトの出力ディレクトリに移動し、選択したビルド構成に応じて [Release] フォルダーまたは [Debug] フォルダーに移動します。 フォルダーのすべてのファイルを、ユーザーがアクセスできる場所にコピーします。

ExcelAddIn セットアップをテストするには

1. **Officeaddinsetup** をにコピーした場所に移動します。
2. setup.exe ファイルをダブルクリックして、 **Officeaddinsetup** アドインをインストールします。 表示されたソフトウェアライセンス条項に同意し、セットアップウィザードを完了して、ユーザーのコンピューターにアドインをインストールします。

Excel Office ソリューションをインストールし、セットアップ時に指定した場所から実行する必要があります。

## <a name="additional-requirements-for-document-level-solutions"></a>ドキュメントレベルのソリューションの追加要件

ドキュメントレベルのソリューションを配置するには、Windows インストーラーセットアッププロジェクトでいくつかの異なる構成手順を実行する必要があります。

ドキュメントレベルのソリューションを配置するために必要な基本的な手順の一覧を次に示します。

- Visual Studio セットアッププロジェクトを作成します。
- ドキュメントレベルのソリューションのプライマリ出力を追加します。 プライマリ出力には、Microsoft Office ドキュメントも含まれています。
- 配置マニフェストとアプリケーションマニフェストをルースファイルとして追加します。
- 依存コンポーネントをインストーラーパッケージから除外します (すべてのユーティリティアセンブリを除く)。
- 前提条件となるパッケージを構成します。
- 起動条件を構成します。
- セットアッププロジェクトをビルドし、結果を配置場所にコピーします。
- セットアップを実行して、ユーザーのコンピューターにドキュメントレベルのソリューションを配置します。
- 必要に応じてカスタムドキュメントのプロパティを更新します。

### <a name="changing-the-location-of-the-deployed-document"></a>配置されたドキュメントの場所の変更

Office ドキュメント内のプロパティは、ドキュメントレベルのソリューションを見つけるために使用されます。 ドキュメントが VSTO アセンブリと同じフォルダーにインストールされている場合は、変更は必要ありません。 ただし、別のフォルダーにインストールされている場合は、セットアップ中にこれらのプロパティを更新する必要があります。

これらのドキュメントプロパティの詳細については、「 [カスタムドキュメントプロパティの概要](custom-document-properties-overview.md)」を参照してください。

これらのプロパティを変更するには、セットアップ中にカスタム動作を使用する必要があります。

次の例では、ExcelWorkbookProject というドキュメントレベルのソリューションと ExcelWorkbookSetup という名前のセットアッププロジェクトを使用します。 ExcelWorkbookSetup プロジェクトは、レジストリキーの設定を除き、上記と同じ手順を使用して構成されます。

カスタムアクションプロジェクトを Visual Studio ソリューションに追加するには

1. 新しい .NET コンソールプロジェクトをソリューションに追加するには、**ソリューションエクスプローラー** で **Office ドキュメント配置プロジェクト** を右クリックします。
2. [ **追加** ] を展開し、[ **新しいプロジェクト**] をクリックします。
3. [コンソールアプリケーション] テンプレートを選択し、プロジェクトに **AddCustomizationCustomAction** という名前を指定します。

    ![ソリューションエクスプローラーのスクリーンショット-AddCustomizationCustomAction](media/setup-project-figure-15.jpg)
  
    **図 12: ソリューションエクスプローラー-AddCustomizationCustomAction**

4. 次のアセンブリへの参照を追加します。
    1. System.ComponentModel
    2. System.Configuration.Install
    3. Microsoft. VisualStudio
    4. Microsoft.VisualStudio.Tools.Applications.ServerDocument

5. このコードを Program.cs または .vb にコピーします。

```csharp
    using System;
    using System.IO;
    using System.Collections;
    using System.ComponentModel;
    using System.Configuration.Install;
    using Microsoft.VisualStudio.Tools.Applications;
    using Microsoft.VisualStudio.Tools.Applications.Runtime;

    namespace AddCustomizationCustomAction
    {
        [RunInstaller(true)]
        public class AddCustomizations : Installer
        {
            public AddCustomizations() : base() { }

            public override void Install(IDictionary savedState)
            {
                base.Install(savedState);

                //Get the CustomActionData Parameters
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;
                string assemblyLocation = Context.Parameters.ContainsKey("assemblyLocation") ? Context.Parameters["assemblyLocation"] : String.Empty;
                string deploymentManifestLocation = Context.Parameters.ContainsKey("deploymentManifestLocation") ? Context.Parameters["deploymentManifestLocation"] : String.Empty;
                Guid solutionID = Context.Parameters.ContainsKey("solutionID") ? new Guid(Context.Parameters["solutionID"]) : new Guid();

                string newDocLocation = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation));

                try
                {
                    //Move the file and set the Customizations
                    if (Uri.TryCreate(deploymentManifestLocation, UriKind.Absolute, out Uri docManifestLocationUri))
                    {
                        File.Move(documentLocation, newDocLocation);
                        ServerDocument.RemoveCustomization(newDocLocation);
                        ServerDocument.AddCustomization(newDocLocation, assemblyLocation,
                                                        solutionID, docManifestLocationUri,
                                                        true, out string[] nonpublicCachedDataMembers);
                    }
                    else
                    {
                        LogMessage("The document could not be customized.");
                    }
                }
                catch (ArgumentException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (DocumentNotCustomizedException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (InvalidOperationException)
                {
                    LogMessage("The customization could not be removed.");
                }
                catch (IOException)
                {
                    LogMessage("The document does not exist or is read-only.");
                }
            }

            public override void Rollback(IDictionary savedState)
            {
                base.Rollback(savedState);
                DeleteDocument();
            }
            public override void Uninstall(IDictionary savedState)
            {
                base.Uninstall(savedState);
                DeleteDocument();
            }
            private void DeleteDocument()
            {
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;

                try
                {
                    File.Delete(Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation)));
                }
                catch (Exception)
                {
                    LogMessage("The document doesn't exist or is read-only.");
                }
            }
            private void LogMessage(string Message)
            {
                if (Context.Parameters.ContainsKey("LogFile"))
                {
                    Context.LogMessage(Message);
                }
            }

            static void Main() { }
            }
    }
```

ドキュメントにカスタマイズを追加するには、VSTO ドキュメントレベルのソリューションのソリューション ID が必要です。 この値は、Visual Studio プロジェクトファイルから取得されます。

ソリューション ID を取得するには

1. [ **ビルド** ] メニューの [ **ソリューションのビルド** ] をクリックして、ドキュメントレベルのソリューションをビルドし、ソリューション ID プロパティをプロジェクトファイルに追加します。
2. **ソリューションエクスプローラー** で、ドキュメントレベルのプロジェクト **ExcelWorkbookProject** を右クリックします。
3. Visual Studio 内からプロジェクトファイルにアクセスするには、[ **UnloadProject** ] をクリックします。

    ![Excel ドキュメントソリューションのアンロードソリューションエクスプローラーのスクリーンショット](media/setup-project-figure-16.jpg)

    **図 13: Excel ドキュメントソリューションのアンロード**

4. **ソリューションエクスプローラー** で、[ **ExcelWorkbookProject** ] を右クリックし、[ **EditExcelWorkbookProject** ] をクリックするか、 **ExcelWorkbookProject を編集** します。
5. **ExcelWorkbookProject** エディターで、 **PropertyGroup** 要素内の **SolutionID** 要素を見つけます。
6. この要素の GUID 値をコピーします。

    ![SolutionID の取得](media/setup-project-figure-17.jpg)

    **図 14: SolutionID を取得する**

7. **ソリューションエクスプローラー** で、[ **ExcelWorkbookProject** ] を右クリックし、[**プロジェクトの再読み込み**] をクリックします。
8. 表示されるダイアログボックスで [ **はい** ] をクリックして、 **ExcelWorkbookProject** エディターを閉じます。
9. **ソリューション ID** は、インストールのカスタムアクションで使用されます。

最後の手順では、 **インストール** と **アンインストール** の手順のカスタム動作を構成します。

### <a name="to-configure-the-setup-project"></a>セットアッププロジェクトを構成するには

1. **ソリューションエクスプローラー** で、[ **ExcelWorkbookSetup**] を右クリックし、[**追加**] を展開して、[**プロジェクト出力**] をクリックします。
2. [ **プロジェクト出力グループの追加** ] ダイアログボックスの [ **プロジェクト** ] ボックスの一覧で、[ **AddCustomizationCustomAction**] をクリックします。
3. [ **プライマリ出力** ] を選択し、[ **OK** ] をクリックしてダイアログボックスを閉じ、カスタムアクションを含むアセンブリをセットアッププロジェクトに追加します。

    ![Document Manifest カスタムアクション-[プロジェクト出力グループの追加] ウィンドウのスクリーンショット](media/setup-project-figure-18.jpg)

    **図 15: ドキュメントマニフェストのカスタムアクション-プロジェクト出力グループの追加**

4. **ソリューションエクスプローラー** で、[ **ExcelWorkbookSetup**] を右クリックします。
5. [ **表示** ] を展開し、[ **カスタムアクション**] をクリックします。
6. [ **カスタムアクション (ExcelWorkbookSetup)** エディター] で、[ **カスタムアクション** ] を右クリックし、[ **カスタムアクションの追加**] をクリックします。
7. [ **プロジェクト内の項目の選択** ] ダイアログボックスの [ **検索対象** ] ボックスの一覧で、[ **アプリケーションフォルダー**] をクリックします。 [ **AddCustomizationCustomAction (アクティブ) からのプライマリ出力** ] を選択し、[ **OK** ] をクリックして、インストール手順にカスタム動作を追加します。
8. [ **インストール] ノード** で、[ **AddCustomizationCustomAction (アクティブ)] の [プライマリ出力**] を右クリックし、[名前の **変更**] をクリックします。 カスタムアクションに " **ドキュメントをコピーする" と** いう名前を付けて、カスタマイズを添付します。
9. [ **アンインストール] ノード** で、[ **AddCustomizationCustomAction (アクティブ) のプライマリ出力** ] を右クリックし、[名前の **変更**] をクリックします。 カスタムアクションに [ドキュメント] フォルダーの [ **ドキュメントの削除**] という名前を指定します。

    ![ドキュメントマニフェストの [カスタムアクション] ウィンドウのスクリーンショット](media/setup-project-figure-19.jpg)

    **図 16: ドキュメントマニフェストのカスタムアクション**

10. [ **カスタムアクション (ExcelWorkbookSetup)** エディター] で、[ **ドキュメントをマイドキュメントにコピー** ] を右クリックし、[カスタマイズのアタッチ] をクリックして、[ **プロパティウィンドウ**] をクリックします。
11. **CustomActionData** の [**プロパティ**] ウィンドウで、カスタマイズ DLL の場所、配置マニフェスト、Microsoft Office ドキュメントの場所を入力します。 SolutionID も必要です。
12. セットアップエラーをファイルに記録する場合は、LogFile パラメーターを含めます。
s
    ``` text
    /assemblyLocation="[INSTALLDIR]ExcelWorkbookProject.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbookProject.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx" /solutionID="Your Solution ID" /LogFile="[TARGETDIR]Setup.log"
    ```

    ![ドキュメントをドキュメントにコピーするカスタムアクションのスクリーンショットプロパティウィンドウ](media/setup-project-figure-20.jpg)

    **図 17: ドキュメントをドキュメントにコピーするカスタムアクション**

13. Uninstall のカスタム動作には、ドキュメントの名前が必要です。 **CustomActionData** の同じ documentlocation パラメーターを使用して指定できます。

    ``` text
    /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx"
    ```

14. **ExcelWorkbookSetup** プロジェクトをコンパイルして配置します。
15. **[マイドキュメント**] フォルダーを探し、ExcelWorkbookProject.xlsx ファイルを開きます。

## <a name="additional-resources"></a>その他のリソース

[方法: Visual Studio Tools for Office ランタイムをインストールする](how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)

[Office Primary Interop Assemblies](office-primary-interop-assemblies.md)

[VSTO アドインのレジストリエントリ](registry-entries-for-vsto-add-ins.md)

[Custom Document Properties Overview](custom-document-properties-overview.md)

[Windows レジストリでのフォーム領域の指定](/office/vba/outlook/concepts/creating-form-regions/specifying-form-regions-in-the-windows-registry)

[Granting Trust to Documents](granting-trust-to-documents.md)

## <a name="about-the-authors"></a>作成者について

Wouter van V氏は、Office Open XML テクノロジを使用した Microsoft MVP であり、SharePoint、Microsoft Office、および関連する .NET テクノロジで Office Business Applications (Oba) を作成することに重点を置いている独立したコンサルタントです。
Wouter は、 [MSDN](/previous-versions/office/developer/office-2007/bb879915(v=office.12))などの開発者コミュニティサイトによく寄せられる共同作成者です。 いくつかのホワイトペーパーや記事を公開しており、「Open XML: 説明済み」というタイトルの本を公開しています。
Wouter は、さまざまなチャネルを通じて最先端の技術コンテンツを配信することを重視しているオランダ企業である創設者のコード弁護士です。 Wouter の詳細については、ブログを参照してください。

Ted のシャードは、SharePoint の MVP、執筆者、トレーナーであり、創設者の Tison グループです。 2005の秋、Ted は Microsoft の Developer Platform エバンジェリズム兼グループによって採用され、Windows SharePoint Services 3.0 および Microsoft Office SharePoint Server 2007 用の Ascend Developer トレーニングカリキュラムを作成しました。 この時間以降、Ted は、SharePoint 2007 テクノロジでプロの開発者を教育することに重点を置いてきました。 Ted は、ビジネスソリューションを構築するための開発プラットフォームとして SharePoint を使用する方法に重点を置いた、Windows SharePoint Services 3.0 内部での Microsoft Press の書籍の作成を完了しました。 Ted は、Office Space という名前の MSDN マガジン用の開発者向けの列も書き込みます。
