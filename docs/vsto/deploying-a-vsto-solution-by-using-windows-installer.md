---
title: Windows インストーラーを使用した Office ソリューション用の Visual Studio ツールの展開
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
ms.openlocfilehash: 46bfa808cbf99e942d7aadd2802f51eecfcefae8
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444907"
---
# <a name="deploying-a-visual-studio-tools-for-office-solution-using-windows-installer"></a>Windows インストーラーを使用した Office ソリューション用の Visual Studio ツールの展開

## <a name="summary"></a>まとめ

Visual Studio インストーラー プロジェクトを使用して Office 用の Microsoft Visual Studio ツール (VSTO) アドインまたはドキュメント レベルのソリューションを展開する方法について説明します。

ウーター・ファン・ヴクト,コード・カウンセル

テッド・パティソン,テッド・パティソン・グループ

この資料は、元の作成者の許可を得てマイクロソフトによって更新されました。

**適用対象:** オフィス、マイクロソフトオフィス、マイクロソフトビジュアルスタジオのためのビジュアルスタジオツール。

## <a name="overview"></a>概要

VSTO ソリューションを開発し、Windows インストーラー パッケージを使用してソリューションを展開できます。 この説明には、簡単な Office アドインを展開する手順が含まれています。

## <a name="deployment-methods"></a>配置方法

ClickOnce を使用すると、アドインとソリューションのセットアップを簡単に作成できます。 ただし、コンピューター レベルのアドインなどの管理者特権を必要とするアドインはインストールできません。

管理者特権を必要とするアドインは、Windows インストーラを使用してインストールできますが、セットアップを作成するにはより多くの労力が必要です。

ClickOnce を使用して VSTO ソリューションを配置する方法の概要については、「 [ClickOnce を使用して Office ソリューションを配置する](deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="deploying-office-solutions-that-target-the-vsto-runtime"></a>VSTO ランタイムを対象とする Office ソリューションの展開

ClickOnce と Windows インストーラー パッケージは、Office ソリューションをインストールするときに同じ基本的なタスクを実行する必要があります。

1. ユーザー のコンピューターに必須コンポーネントをインストールします。
2. ソリューションの特定のコンポーネントを展開します。
3. アドインの場合は、レジストリ エントリを作成します。
4. ソリューションを信頼して実行できるようにします。

### <a name="required-prerequisite-components-on-the-target-computer"></a>ターゲット コンピュータで必要な必須コンポーネント

VSTO ソリューションを実行するためにコンピュータにインストールする必要があるソフトウェアの一覧を次に示します。

- マイクロソフトオフィス2010以降。
- .NET フレームワーク 4 以降。
- Microsoft Visual Studio 2010 Tools for Office Runtime
  ランタイムは、アドインとドキュメント レベルのソリューションを管理する環境を提供します。 ランタイムのバージョンは Microsoft Office に付属していますが、アドインと共に特定のバージョンを再配布することもできます。
- 埋め込み相互運用機能の種類を使用していない場合は、Microsoft Office のプライマリ相互運用機能アセンブリ。
- プロジェクトによって参照されるユーティリティ アセンブリ。

### <a name="specific-components-for-the-solution"></a>ソリューションの特定のコンポーネント

インストーラ パッケージは、次のコンポーネントをユーザーのコンピュータにインストールする必要があります。

- ドキュメント レベルのソリューションを作成する場合は、Office ドキュメントを作成します。
- カスタマイズ アセンブリと、必要なアセンブリ。
- 構成ファイルなどの追加コンポーネント。
- アプリケーション マニフェスト (.manifest)
- 配置マニフェスト (.vsto)

### <a name="registry-entries-for-add-ins"></a>アドインのレジストリ エントリ

Office では、レジストリ エントリを使用してアドインを検索し、読み込みます。これらのレジストリ エントリは、展開プロセスの一部として作成する必要があります。 これらのレジストリ エントリの詳細については、「 [VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

カスタム フォーム領域を表示する Outlook アドインでは、フォーム領域を識別するための追加のレジストリ エントリが必要です。 レジストリ エントリの詳細については、「 [Outlook フォーム領域のレジストリ エントリ](registry-entries-for-vsto-add-ins.md#OutlookEntries)」を参照してください。

ドキュメント レベルのソリューションでは、レジストリ エントリは必要ありません。 代わりに、ドキュメント内のプロパティを使用してカスタマイズを検索します。 これらのプロパティの詳細については、「[カスタム ドキュメント プロパティの概要](custom-document-properties-overview.md)」を参照してください。

### <a name="trusting-the-vsto-solution"></a>VSTO ソリューションを信頼する

カスタマイズを実行するには、ソリューションがコンピューターによって信頼されている必要があります。 アドインは、証明書を使用してマニフェストに署名するか、信頼リストとの信頼関係を作成するか、またはコンピューター上の信頼できる場所にインストールすることによって信頼できます。

署名用の証明書を取得する方法の詳細については、「 [ClickOnce の配置と認証の方法](../deployment/clickonce-and-authenticode.md)」を参照してください。 ソリューションの信頼の詳細については、「[包含リストを使用して Office ソリューションを信頼する](trusting-office-solutions-by-using-inclusion-lists.md)」を参照してください。 Windows インストーラ ファイルにカスタム動作を含む対象リスト エントリを追加できます。 包含リストを有効にする方法の詳細については、「[方法 : 包含リスト セキュリティを構成する](how-to-configure-inclusion-list-security.md)」を参照してください。

どちらのオプションも使用しない場合は、ソリューションを信頼するかどうかをユーザーに決定させる信頼プロンプトが表示されます。

ドキュメント レベルのソリューションに関連するセキュリティの詳細については、「[ドキュメントに対する信頼の付与](granting-trust-to-documents.md)」を参照してください。

## <a name="creating-a-basic-installer"></a>基本インストーラの作成

セットアップ プロジェクト テンプレートと配置プロジェクト テンプレートは、ダウンロード可能な[Microsoft Visual Studio インストーラー プロジェクト](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects)拡張機能に含まれています。

Office ソリューションのインストーラーを作成するには、次の作業を実行する必要があります。

- 展開する Office ソリューションのコンポーネントを追加します。
- アプリケーション レベルのアドインの場合は、レジストリ キーを構成します。
- エンド ユーザーのコンピュータにインストールできるように、前提条件コンポーネントを構成します。
- 起動条件を設定して、必要な前提条件コンポーネントが使用可能であることを確認します。 必要な前提条件がすべてインストールされていない場合は、起動条件を使用してインストールをブロックできます。

最初の手順は、セットアップ プロジェクトを作成することです。

### <a name="to-create-the-addin-setup-project"></a>アドイン セットアップ プロジェクトを作成するには

1. 展開する Office アドイン プロジェクトを開きます。 この例では、ExcelAddIn という名前の Excel アドインを使用しています。
2. Office プロジェクトを開いた場合は、[**ファイル]** メニューの [**追加**] を展開し、[**新しいプロジェクト**] をクリックして新しいプロジェクトを追加します。
::: moniker range="=vs-2017"
3. [**新しいプロジェクトの追加**] ダイアログで、[プロジェクトの種類] ペインの **[その他のプロジェクトの種類**] を展開し、[**セットアップと配置**] を展開して **、[Visual Studio インストーラー**] を選択します。 **the Project types**
4. [**テンプレート]** ウィンドウで **、[Visual Studio がインストールされている**テンプレート] グループから [**セットアップ プロジェクト**] を選択します。
::: moniker-end
::: moniker range="=vs-2019"
3. [**新しいプロジェクトの追加**]ダイアログ で、[**プロジェクトのセットアップ]** テンプレートを選択します。
4. **[次へ]** をクリックします。
::: moniker-end

5. [**名前]** ボックス**に「OfficeAddInSetup」** と入力します。
::: moniker range="=vs-2017"
6. [**開く**] をクリックして、新しいセットアップ プロジェクトを作成します。
::: moniker-end
::: moniker range="=vs-2019"
6. [**作成**] をクリックして、新しいセットアップ プロジェクトを作成します。
::: moniker-end

Visual Studio は、新しいセットアップ プロジェクトのファイル システム エクスプローラーを開きます。 ファイル システム エクスプローラでは、セットアップ プロジェクトにファイルを追加できます。

   ![セットアップ プロジェクトのファイル システム エクスプローラーのスクリーンショット](media/setup-project-figure-1.png)

   **図 1: セットアップ プロジェクトのファイル システム エクスプローラ**

セットアップ プロジェクトは、ExcelAddIn を配置する必要があります。 このタスクのセットアップ プロジェクトを構成するには、ExcelAddIn プロジェクト出力をセットアップ プロジェクトに追加します。

### <a name="to-add-the-exceladdin-project-output"></a>プロジェクト出力を追加するには

1. ソリューション**エクスプローラ**で、[ **OfficeAddInSetup**] を右クリックし、[**追加**]、[**プロジェクト出力**] の順にクリックします。
2. [**プロジェクト出力グループの追加**] ダイアログで、プロジェクトリストから**ExcelAddIn**を選択し、**プライマリ出力を選択**します。
3. **[OK] を**クリックして、プロジェクト出力をセットアップ プロジェクトに追加します。

    ![[プロジェクトのセットアップ] [プロジェクト出力グループの追加] ダイアログ のスクリーンショット](media/setup-project-figure-2.png)

    **図 2: プロジェクトのセットアップ プロジェクトの [プロジェクト出力グループの追加] ダイアログ**

セットアップ プロジェクトは、配置マニフェストとアプリケーション マニフェストを配置する必要があります。 ExcelAddIn プロジェクトの出力フォルダーからスタンドアロン ファイルとして、セットアップ プロジェクトにこれらの 2 つのファイルを追加します。

### <a name="to-add-the-deployment-and-application-manifests"></a>配置マニフェストとアプリケーション マニフェストを追加するには

1. ソリューション**エクスプローラ**で **、[OfficeAddInSetup]** を右クリックし、[**追加**]**をクリックします**。
2. [**ファイルの追加]** ダイアログ ボックスで **、ExcelAddIn**出力ディレクトリに移動します。 通常、出力ディレクトリは、選択したビルド構成に応じて、プロジェクトルートディレクトリの**bin\\release**サブフォルダーです。
3. **ExcelAddIn.vsto**ファイルと**ExcelAddIn.dll.manifest.manifest**ファイルを選択し、[**開く**] をクリックして、これらの 2 つのファイルをセットアップ プロジェクトに追加します。

    ![ソリューション エクスプローラーでのアプリケーション マニフェストと配置マニフェストのスクリーンショット](media/setup-project-figure-3.jpg)

    **図 3: ソリューション エクスプローラーでアドインのアプリケーション マニフェストと配置マニフェスト**

ExcelAddIn を参照すると、ExcelAddIn で必要なすべてのコンポーネントが含まれます。 これらのコンポーネントは、正しく登録できるように、前提条件パッケージを使用して除外および展開する必要があります。 また、インストールを開始する前にソフトウェア ライセンス条項を表示し、同意する必要があります。

### <a name="to-exclude-the-exceladdin-project-dependencies"></a>ExcelAddIn プロジェクトの依存関係を除外するには

1. ソリューション**エクスプローラー**の **[OfficeAddInSetup]** ノードで、[**検出された依存関係**] 項目の下のすべての依存関係**項目を選択****\*します。ユーティリティ.dll**. ユーティリティ アセンブリは、アプリケーションと共に配置されます。
2. グループを右クリックし、[**プロパティ ]** を選択します。
3. [**プロパティ]** ウィンドウで、セットアップ プロジェクトから依存アセンブリを**除外するには、Exclude**プロパティを**True**に変更します。 ユーティリティ アセンブリは除外しないでください。

    ![除外する依存関係を示すソリューション エクスプローラーのスクリーンショット](media/setup-project-figure-4.jpg)

    **図 4: 依存関係の除外**

Windows インストーラ パッケージを構成して、ブートストラップとも呼ばれるセットアップ プログラムを追加して、必須コンポーネントをインストールできます。 このセットアップ プログラムは、ブートストラップと呼ばれるプロセスの前提条件コンポーネントをインストールできます。

**ExcelAddIn**の場合、アドインを正しく実行するには、次の前提条件をインストールする必要があります。

- Office ソリューションが対象とするバージョンです。
- Microsoft Visual Studio 2010 Tools for Office Runtime。

依存コンポーネントを必須コンポーネントとして構成するには

1. ソリューション**エクスプローラ**で **、OfficeAddInSetup**プロジェクトを右クリックし、[**プロパティ]** をクリックします。
2. **[OfficeAddInSetup プロパティ ページ**] ダイアログ ボックスが表示されます。
3. [**前提条件]** ボタンをクリックします。
4. [必須コンポーネント] ダイアログ ボックスで、Office ランタイム用の .NET フレームワークと Visual Studio ツールの正しいバージョンを選択します。

    ![[必須コンポーネント] ダイアログ ボックスのスクリーンショット](media/setup-project-figure-5.png)

    **図 5: [必須コンポーネント] ダイアログ ボックス**

    > [!NOTE]
    >Visual Studio セットアップ プロジェクトで構成されている前提条件パッケージの一部は、選択したビルド構成に依存しています。 使用する各ビルド構成に対して、適切な前提条件コンポーネントを選択する必要があります。

レジストリ キーを使用してアドインを検索します。 HKEY\_現在\_のユーザー ハイブのキーは、個々のユーザーのアドインを登録するために使用されます。 HKEY\_LOCAL\_MACHINE ハイブの下のキーは、マシンのすべてのユーザーのアドインを登録するために使用されます。 レジストリ キーの詳細については、「 [VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

### <a name="to-configure-the-registry"></a>レジストリを構成するには

1. ソリューション**エクスプローラ**で、[ **OfficeAddInSetup**] を右クリックします。
2. [**表示 ]** を展開します。
3. [**レジストリ]** をクリックしてレジストリ エディタ ウィンドウを開きます。
4. レジストリ **(OfficeAddInSetup)** エディターで **、HKEY\_\_ローカル コンピューター**を展開し、**次にソフトウェアを展開**します。
5. **HKEY\_ローカル\_\\マシン ソフトウェア**の**\[\]** 下にある製造元の ?キーを削除します。
6. **HKEY\_現在\_のユーザー**を展開し、**ソフトウェア**を展開します。
7. **HKEY\_現在\_\\**の**\[\]** ユーザー ソフトウェアの下にある製造元のキーを削除します。
8. アドイン インストールのレジストリ キーを追加するには、**ユーザー/マシン ハイブ**キーを右クリックし、[**新しいキー**] をクリックします。 新しいキーの名前には **「ソフトウェア」** というテキストを使用します。 新しく作成した**ソフトウェア**キーを右クリックし、 **Microsoft**というテキストを使用して新しいキーを作成します。
9. 同様のプロセスを使用して、アドイン登録に必要なキー階層全体を作成します。

    **ユーザー/マシンハイ\\ブ\\ソフトウェア\\マイクロソフト\\オフィス\\エクセルアドイン\\サンプルカンパニー.ExcelAddIn**

    会社名は、一意性を提供するアドインの名前のプレフィックスとしてよく使用されます。

10. **キー**を右クリックし、[**新規作成**] をクリックして、[**文字列値**] をクリックします。 名前の**テキストを使用して説明**します。
11. このステップを使用して、さらに 3 つの値を追加します。
    - 文字列**型の****フレンドリ名**
    - **DWORD 型の読み込み動作****DWORD**
    - **文字列**型の**String**マニフェスト

12. レジストリ エディタで [**説明**] の値を右クリックし、[**プロパティ ウィンドウ**] をクリックします。 [**プロパティ] ウィンドウ**で、[値] プロパティ**に「Excel デモ アドイン**」と入力します。
13. レジストリ エディタで **[フレンドリ名**]キーを選択します。 [**プロパティ] ウィンドウ**で、**値**プロパティを**Excel デモ アドイン**に変更します。
14. レジストリ エディタで**LoadBehavior**キーを選択します。 **[プロパティ] ウィンドウ**で **、Value**プロパティを 3 に変更**します。** LoadBehavior の値 3 は、ホスト アプリケーションの起動時にアドインを読み込む必要があることを示します。 読み込み動作の詳細については、「 [VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

15. レジストリ エディターで **[マニフェスト]** キーを選択します。 [**プロパティ] ウィンドウ**で、[**値**] プロパティを**ファイルに**変更します。

    ![レジストリ エディタのスクリーンショット](media/setup-project-figure-6.png)

    **図 6: レジストリ キーの設定**

      VSTO ランタイムは、このレジストリ キーを使用して配置マニフェストを見つけます。 [TARGETDIR] マクロは、アドインのインストール先のフォルダーに置き換えられます。 マクロには末尾の \ 文字が含まれるため、配置マニフェストのファイル名は \文字を除いた ExcelAddIn.vsto にする必要があります。
      **vstolocal**ポストフィックスは、アドインが ClickOnce キャッシュの代わりにこの場所から読み込む必要があることを VSTO ランタイムに通知します。 この接尾辞を削除すると、ランタイムはカスタマイズを ClickOnce キャッシュにコピーします。

   >[!WARNING]
   >Visual Studio のレジストリ エディタには、細心の注意が必要です。 たとえば、誤って誤ったキーに DeleteAtUninstall を設定した場合、レジストリのアクティブな部分を削除し、ユーザーのコンピュータが矛盾した状態、あるいはさらに悪い状態のままになることがあります。

64 ビット バージョンの Office では、64 ビット レジストリ ハイブを使用してアドインを検索します。64 ビット レジストリ ハイブでアドインを登録するには、セットアップ プロジェクトのターゲット プラットフォームを 64 ビットのみに設定する必要があります。

1. ソリューション エクスプローラーで**OfficeAddInSetup**プロジェクトを選択します。
2. **[プロパティ]** ウィンドウに移動し、[**ターゲット プラットフォーム**] プロパティを **[x64]** に設定します。

32 ビット版と 64 ビット版の Office の両方に対してアドインをインストールするには、2 つの別個の MSI パッケージを作成する必要があります。 32 ビット用と 64 ビット用の 1 つ。

  ![64 ビット Office にアドインを登録するためのターゲット プラットフォームを示す [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-7.jpg)

  **図 7: 64 ビット Office にアドインを登録するためのターゲット プラットフォーム**

MSI パッケージを使用してアドインまたはソリューションをインストールする場合、必要な必須コンポーネントをインストールせずにインストールされる場合があります。 MSI の起動条件を使用して、前提条件がインストールされていない場合にアドインのインストールをブロックできます。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime"></a>VSTO ランタイムを検出するための起動条件の構成

1. ソリューション**エクスプローラ**で、[ **OfficeAddInSetup**] を右クリックします。
2. [**表示 ]** を展開します。
3. [**起動条件]** をクリックします。
4. **起動条件 (OfficeAddInSetup)** エディターで、ターゲット**コンピューターの要件**を右クリックし、**レジストリ起動条件の追加**] をクリックします。 この検索条件は、VSTO ランタイムがインストールするキーをレジストリで検索できます。 キーの値は、名前付きプロパティを通じてインストーラーのさまざまな部分で使用できます。 起動条件では、検索条件で定義されたプロパティを使用して、特定の値をチェックします。
5. **起動条件 (OfficeAddInSetup)** エディターで、**レジストリEntry1 の検索**検索条件を選択し、条件を右クリックして、**プロパティ ウィンドウ**を選択します。

6. **[プロパティ]** ウィンドウで、次のプロパティを設定します。
   1. **[(名前)]** の値を **[VSTO 2010 ランタイムの検索**] に設定します。
   2. **プロパティ**の値を**VSTORUNTIMEREDIST**に変更します。
   3. **ソフトウェア****\\マイクロソフト VSTO ランタイム\\セットアップ v4R にレジストリ キーの値を設定\\します。**
   4. **Root**プロパティは**vsdrrHKLM**に設定したままにします。
   5. **"値**" プロパティを **[バージョン]** に変更します。

7. **起動条件 (OfficeAddInSetup)** エディターで **、Condition1**の起動条件を選択し、条件を右クリックして、 **[ プロパティ ウィンドウ ]** を選択します。
8. [プロパティ] ウィンドウで、次のプロパティを設定します。
   1. **(名前) を** **VSTO 2010 ランタイムの可用性を確認**する に設定します。
   2. **条件**の値を**VSTORUNTIMEREDIST\>="10.0.30319" に変更します。**
   3. **"InstallURL/インストール URL"** プロパティは空白のままにします。
   4. **Office** **ランタイム用の Visual Studio 2010 ツールがインストールされていないにメッセージを設定します。Setup.exe を実行してアドインをインストールしてください**。

        ![ランタイムの可用性の確認の起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-8.jpg)

        **図 8: 実行時の可用性の確認の起動条件の [プロパティ] ウィンドウ**

 上記の起動条件は、ブートストラップ パッケージによってインストールされるときに、VSTO ランタイムの存在を明示的にチェックします。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime-installed-by-office"></a>Office によってインストールされた VSTO ランタイムを検出する起動条件を構成する

1. **起動条件 (OfficeAddInSetup)** エディタで、[ターゲット**コンピュータの検索**] を右クリックし、[**レジストリ検索の追加**] をクリックします。
2. レジストリ**エントリ1の検索**検索条件を選択し、条件を右クリックして、[プロパティ**ウィンドウ**] を選択します。
3. **[プロパティ]** ウィンドウで、次のプロパティを設定します。
    1. **(名前)** の値を**Office VSTO ランタイムの検索**に設定します。
    2. **プロパティ**の値を**Office ランタイム**に変更します。
    3. **レジストリ キー**の値を**ソフトウェア\\マイクロソフト\\VSTO\\ランタイム セットアップ v4**に設定します。
    4. **Root**プロパティは**vsdrrHKLM**に設定したままにします。
    5. **"値**" プロパティを **[バージョン]** に変更します。

4. **起動条件 (OfficeAddInSetup)** エディターで、前に定義した**VSTO 2010 ランタイムの起動**条件を確認するを選択し、条件を右クリックして、**プロパティ ウィンドウ**を選択します。

5. **条件**プロパティの値を**VSTORUNTIMEREDIST \>="10.0.30319" または OFFICERUNTIME\>="10.0.21022" に**変更します。 アドインで必要なランタイムのバージョンによっては、バージョン番号が異なる場合があります。

    ![起動条件のプロパティ ウィンドウのスクリーンショット](media/setup-project-figure-9.jpg)
  
    **図 9: Redist または Office の起動条件を使用してランタイムの可用性を確認するプロパティウィンドウ**

アドインが .NET Framework 4 以降を対象とする場合、参照されているプライマリ相互運用機能アセンブリ (PIA) 内の型を VSTO アセンブリに埋め込むことができます。

次の手順を実行して、相互運用機能の種類がアドインに埋め込まれるかどうかを確認するには、次の手順を実行します。

1. ソリューション エクスプローラーで [参照] ノードを展開する
2. PIA 参照の 1 つを**選択します。**
3. F4 キーを押すか、[アセンブリ] コンテキスト メニューから [プロパティ] を選択して、プロパティ ウィンドウを表示します。
4. プロパティの "**相互運用機能型の埋め込み" の**値を確認します。

値が**True**に設定されている場合は、型が埋め込まれているので、[**セットアップ プロジェクトをビルドするには**](#to-build-the-setup-project)」 セクションに進むことができます。

詳細については、「[型の等価性」および「埋め込み相互運用型」を参照してください。](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)

### <a name="to-configure-launch-conditions-to-detect-that-for-office-pias"></a>Office PIA 用に起動条件を検出するように構成するには

1. **起動条件 (OfficeAddInSetup)** エディターで、ターゲット**コンピューターの要件**を右クリックし **、Windows インストーラーの起動条件の追加] をクリック**します。 この起動条件は、特定のコンポーネント ID を検索して Office PIA を検索します。
2. **[Component1 の検索**]を右クリックし、[**プロパティ]ウィンドウ**をクリックして、起動条件のプロパティを表示します。
3. **[プロパティ] ウィンドウ**で、次のプロパティを設定します。

    1. **(名前)** プロパティの値を**Office 共有 PIA の検索**に変更する
    2. 使用している Office**コンポーネントのコンポーネント ID**の値を [コンポーネント ID] に変更します。 コンポーネント ID のリストは **、{64E2917E-AA13-4CA4-BFFE-EA6EDA3AF4}** など、次の表で確認できます。
    3. **プロパティ**の値を **[HASSHAREDPIA]** に変更します。

4. **起動条件 (OfficeAddInSetup)** エディターで、条件**1**を右クリックし、**プロパティ ウィンドウ**をクリックして起動条件のプロパティを表示します。

5. **Condition1**のこれらのプロパティを変更します。

    1. **(名前) を** **「Office 共有 PIA の可用性を確認**する」に変更します。
    2. **条件**を **[HASSHAREDPIA]** に変更します。
    3. **インストール Url を**空白のままにします。
    4. Excel**Message****との対話に必要なコンポーネントをメッセージに変更することはできません。setup.exe を実行してください**。

    ![Office 共有 PIA の起動条件の確認の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-10.jpg)
  
    **図 10: Office 共有 PIA 起動状態の確認の [プロパティ] ウィンドウ**

### <a name="component-ids-of-the-primary-interop-assemblies-for-microsoft-office"></a>Office のプライマリ相互運用機能アセンブリのコンポーネント ID

|プライマリ相互運用機能アセンブリ|Office 2010|Office 2013|オフィス 2013 (64 ビット)|Office 2016|オフィス 2016 (64 ビット)|
|------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|
|Excel|{EA7564AC-C67D-4868-BE5C-26E4FC2223FF}|{C8A65ABE-3270-4FD7-B854-50C8082C8F39}|{E3BD1151-B9CA-4D45-A77E-51A6E0ED322A}|C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|{C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|
|InfoPath|{4153F732-D670-4E44-8AB7-500F2B576BDA}|{0F825A16-25B2-4771-A497-FC8AF3B355D8}|{C5BBD36E-B320-47EF-A512-556B99CB7E41}|-|-|
|Outlook|{1D844339-3DAE-413E-BC13-62D6A52816B2}|{F9F828D5-9F0B-46F9-9E3E-9C59F3C5E136}|{7824A03F-28CC-4371-BC54-93D15EFC1E7F}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|
|PowerPoint|{EECBA6B8-3A62-44AD-99EB-8666265466F9}|{813139AD-6DAB-4DDD-8C6D-0CA30D07B41}|{05758318-BCFD-4288-AD8D-81185841C235}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|
|Visio|{3EA123B5-6316-452E-9D51-A489E06E2347}|{C1713368-12A8-41F1-ACA1-934B01AD6EEB}|{2CC0B221-22D2-4C15-A9FB-DE818E51AF75}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|
|Word|{8B74A499-37F8-4DEA-B5A0-D72FC501CEFA}|{9FE736B7-B1EE-410C-8D07-082891C3DAC8}|{13C07AF5-B206-4A48-BB5B-B8022333E3CA}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|
|マイクロソフト フォーム 2.0|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{A5A30117-2D2A-4C5C-B3C8-8897AC32C2AC}|-|-|
|Microsoft Graph|{011B9112-EBB1-4A6C-86CB-C2FDC9EA7B0E}|{52DA4B37-B8EB-4B7F-89C1-824654CE4C70}|{24706F33-F0CE-4EB4-BC91-9E935394F510}|-|-|
|スマート タグ|{7102C98C-EF47-4F04-A227-FE33650BF954}|{487A7921-EB3A-4262-BB5B-A5736B732486}|{74EFC1F9-747D-4867-B951-EFCF29F51AF7}|-|-|
|オフィス共有|{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}|{6A174BDB-0049-4D1C-86EF-3114CB0C4C4E}|{76601EBB-44A7-49EE-8DE3-7B7B9D7EBB05}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|
|Project|{957A4EC0-E67B-4E86-A383-6AF7270B216A}|{1C50E422-24FA-44A9-A120-E88280C8C341}|{706D7F44-8231-489D-9B25-3025ADE9F114}|{107BCD9A-F1DC-4004-A444-33706FC10058}|{107BCD9A-F1DC-4004-A444-33706FC10058}|

  ![最終起動条件のスクリーンショット](media/setup-project-figure-11.jpg)

  **図 11: 最終起動条件**

ExcelAddIn インストールの起動条件をさらに詳細に設定できます。 たとえば、実際のターゲット Office アプリケーションがインストールされているかどうかを確認すると便利です。

### <a name="to-build-the-setup-project"></a>セットアップ プロジェクトをビルドするには

1. ソリューション**エクスプローラ**で **、OfficeAddInSetup**プロジェクトを右クリックし、[**ビルド**] をクリックします。
2. **Windows エクスプローラ**を使用して **、OfficeAddInSetup**プロジェクトの出力ディレクトリに移動し、選択したビルド構成に応じて[リリース]または[デバッグ]フォルダに移動します。 フォルダ内のすべてのファイルを、ユーザーがアクセスできる場所にコピーします。

セットアップをテストするには

1. コピー先に移動**します**。
2. setup.exe ファイルをダブルクリックして **、OfficeAddInSetup**アドインをインストールします。 表示されたソフトウェア ライセンス条項に同意し、セットアップ ウィザードを完了して、ユーザー のコンピュータにアドインをインストールします。

Excel Office ソリューションは、セットアップ中に指定された場所からインストールおよび実行する必要があります。

## <a name="additional-requirements-for-document-level-solutions"></a>ドキュメント レベルのソリューションに関するその他の要件

ドキュメント レベルのソリューションを展開するには、Windows インストーラ セットアップ プロジェクトでいくつかの異なる構成手順が必要です。

ドキュメント レベルのソリューションを展開するために必要な基本的な手順の一覧を次に示します。

- Visual Studio セットアップ プロジェクトを作成します。
- ドキュメント レベルのソリューションのプライマリ出力を追加します。 プライマリ出力には、Microsoft Office ドキュメントも含まれます。
- 展開マニフェストとアプリケーション マニフェストをルーズ ファイルとして追加します。
- 依存コンポーネントをインストーラー パッケージから除外します (ユーティリティ アセンブリを除く)。
- 前提条件パッケージを構成します。
- 起動条件を設定します。
- セットアップ プロジェクトをビルドし、結果を配置場所にコピーします。
- セットアップを実行して、ユーザー コンピューターにドキュメント レベルのソリューションを展開します。
- 必要に応じて、カスタム ドキュメント プロパティを更新します。

### <a name="changing-the-location-of-the-deployed-document"></a>配置されたドキュメントの場所の変更

Office ドキュメント内のプロパティは、ドキュメント レベルのソリューションを検索するために使用されます。 ドキュメントが VSTO アセンブリと同じフォルダーにインストールされている場合、変更は不要です。 ただし、別のフォルダーにインストールされている場合は、これらのプロパティをセットアップ中に更新する必要があります。

これらのドキュメント プロパティの詳細については、「[カスタム ドキュメント プロパティの概要](custom-document-properties-overview.md)」を参照してください。

これらのプロパティを変更するには、セットアップ中にカスタム アクションを使用する必要があります。

次の例では、ExcelWorkbookProject という名前のドキュメント レベルのソリューションと、ExcelWorkbookSetup という名前のセットアップ プロジェクトを使用しています。 ExcelWorkbookSetup プロジェクトは、レジストリ キーを設定する以外は、上記と同じ手順を使用して構成されます。

カスタム アクション プロジェクトを Visual Studio ソリューションに追加するには

1. ソリューション エクスプローラーで**Office ドキュメントの展開**プロジェクトを右クリックして、ソリューションに新しい .NET コンソール プロジェクトを追加**します。**
2. [**追加]** を展開し、[**新しいプロジェクト**] をクリックします。
3. コンソール アプリケーション テンプレートを選択し、プロジェクトに名前を付**けるカスタマイズカスタム アクション**。

    ![ソリューション エクスプローラーのスクリーンショット - カスタマイズカスタム アクションの追加](media/setup-project-figure-15.jpg)
  
    **図 12: ソリューション エクスプローラー - カスタマイズの追加カスタム アクション**

4. 次のアセンブリに参照を追加します。
    1. System.ComponentModel
    2. System.Configuration.Install
    3. アプリケーション
    4. Microsoft.VisualStudio.Tools.Applications.ServerDocument

5. このコードをProgram.csまたは Program.vb にコピーします

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

カスタマイズをドキュメントに追加するには、VSTO ドキュメント レベルのソリューションのソリューション ID が必要です。 この値は、Visual Studio プロジェクト ファイルから取得されます。

ソリューション ID を取得するには

1. [**ビルド**] メニューの [**ソリューションのビルド**] をクリックしてドキュメント レベルのソリューションをビルドし、ソリューション ID プロパティをプロジェクト ファイルに追加します。
2. ソリューション**エクスプローラー**で、ドキュメント レベルのプロジェクト**ExcelWorkbookProject**を右クリックします。
3. プロジェクト ファイルにアクセスするには、プロジェクトの**アンロード**をクリックします。

    ![ソリューション エクスプローラーのアンロード Excel ドキュメント ソリューションのスクリーンショット](media/setup-project-figure-16.jpg)

    **図 13: Excel ドキュメント ソリューションのアンロード**

4. ソリューション**エクスプローラー**で **、Excel ブック プロジェクト**を右クリックし、[**編集]** をクリック**します。**
5. **エディターで**、**プロパティグループ**要素内の**ソリューション ID**要素を見つけます。
6. この要素の GUID 値をコピーします。

    ![ソリューション ID の取得](media/setup-project-figure-17.jpg)

    **図 14: ソリューション ID の取得**

7. ソリューション**エクスプローラー**で **、ExcelWorkbookProject**を右クリックし、[**プロジェクトの再読み込み**] をクリックします。
8. 表示されるダイアログ ボックスで [**はい**] をクリックして **、ExcelWorkbookProject**エディターを閉じます。
9. **ソリューション ID**は、カスタム 動作のインストールで使用されます。

最後の手順では、**インストール**と**アンインストール**の手順のカスタム アクションを構成します。

### <a name="to-configure-the-setup-project"></a>セットアップ プロジェクトを構成するには

1. ソリューション**エクスプローラ**で **、[ExcelWorkbookSetup]** を右クリックし、[**追加**] を展開して [**プロジェクト出力**] をクリックします。
2. [**プロジェクト出力グループの追加**] ダイアログ ボックスの [**プロジェクト**] ボックスの一覧で、[**カスタマイズの追加アクション**] をクリックします。
3. **[プライマリ出力**]を選択し **、[OK]を**クリックしてダイアログ ボックスを閉じ、カスタム アクションを含むアセンブリをセットアップ プロジェクトに追加します。

    ![ドキュメント マニフェストのカスタム アクションのスクリーンショット - プロジェクト出力グループの追加] ウィンドウ](media/setup-project-figure-18.jpg)

    **図 15: ドキュメント マニフェストのカスタム アクション - プロジェクト出力グループの追加**

4. ソリューション**エクスプローラ**で **、ExcelWorkbookSetup**を右クリックします。
5. [**表示]** を展開し、[**カスタム動作**] をクリックします。
6. カスタム**動作 (ExcelWorkbookSetup)** エディターで、[**カスタム動作**] を右クリックし、[**カスタム動作の追加**] をクリックします。
7. [**プロジェクトの項目の選択**] ダイアログ ボックス**の [ファイルの場所**] ボックスの一覧で、[**アプリケーション フォルダ**] をクリックします。 [**カスタマイズのカスタムアクションの追加](active)から[プライマリ出力**]を選択し **、[OK]を**クリックしてカスタムアクションをインストールステップに追加します。
8. [**インストール**] ノードで、[**カスタマイズのカスタマイズアクション (アクティブ) のプライマリ出力**] を右クリックし、[**名前の変更**] をクリックします。 カスタム アクションに **[マイ ドキュメントにドキュメントをコピーしてカスタマイズを添付] という名前を付けます**。
9. [アンインストール]**ノード**で、[**カスタマイズのカスタマイズアクションの追加( アクティブ)] の [プライマリ出力**] を右クリックし、[**名前の変更**] をクリックします。 カスタム アクションに **[ドキュメント フォルダからドキュメントを削除] という名前を付けます**。

    ![[ドキュメント マニフェストのカスタム アクション] ウィンドウのスクリーンショット](media/setup-project-figure-19.jpg)

    **図 16: ドキュメント マニフェストのカスタム アクション**

10. カスタム**動作 (ExcelWorkbookSetup)** エディターで、[**マイ ドキュメントにドキュメントをコピーしてカスタマイズを添付**する] を右クリックし、[**プロパティ ウィンドウ]** をクリックします。
11. **[CustomActionData** **プロパティ]** ウィンドウで、カスタマイズ DLL の場所、配置マニフェスト、および Microsoft Office ドキュメントの場所を入力します。 ソリューション ID も必要です。
12. セットアップ エラーをファイルに記録する場合は、LogFile パラメータを指定します。
s
    ``` text
    /assemblyLocation="[INSTALLDIR]ExcelWorkbookProject.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbookProject.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx" /solutionID="Your Solution ID" /LogFile="[TARGETDIR]Setup.log"
    ```

    ![[マイ ドキュメント プロパティ] ウィンドウにドキュメントをコピーするカスタム アクションのスクリーンショット](media/setup-project-figure-20.jpg)

    **図 17: ドキュメントをマイ ドキュメントにコピーするカスタム アクション**

13. アンインストールのカスタム アクションにはドキュメントの名前が必要です。 **CustomActionData**

    ``` text
    /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx"
    ```

14. プロジェクトをコンパイルして配置**します**。
15. **[マイ ドキュメント]** フォルダーを検索し、ExcelWorkbookProject.xlsx ファイルを開きます。

## <a name="additional-resources"></a>その他のリソース

[方法 : Office ランタイム用の Visual Studio ツールをインストールする](how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)

[オフィス プライマリ相互運用機能アセンブリ](office-primary-interop-assemblies.md)

[VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)

[Custom Document Properties Overview](custom-document-properties-overview.md)

[Windows レジストリでのフォーム領域の指定](/office/vba/outlook/concepts/creating-form-regions/specifying-form-regions-in-the-windows-registry)

[Granting Trust to Documents](granting-trust-to-documents.md)

## <a name="about-the-authors"></a>作成者について

Wouter van Vugt は、Office オープン XML テクノロジを持つマイクロソフト MVP であり、独立したコンサルタントであり、SharePoint、マイクロソフト オフィス、および関連する .NET テクノロジを使用して Office ビジネス アプリケーション (OBA) を作成することに重点を置いています。
Wouter は MSDN などの開発者コミュニティ サイトに頻繁に貢献[しています](/previous-versions/office/developer/office-2007/bb879915(v=office.12))。 彼はいくつかのホワイトペーパーや記事を出版し、Open XML: 説明された電子書籍というタイトルの本を掲載しています。
Wouterは、さまざまなチャネルを通じて最先端の技術コンテンツを提供することに焦点を当てたオランダのCode-Counselの創設者です。 あなたは彼のブログを読んでWouterについての詳細を知ることができます。

テッド・パティソンはSharePoint MVP、著者、トレーナー、テッド・パティソン・グループの創設者です。 2005 年秋、テッドはマイクロソフトの開発者プラットフォーム伝道グループに採用され、Windows SharePoint サービス 3.0 および Microsoft Office SharePoint Server 2007 のアセンド開発者トレーニング カリキュラムを作成しました。 それ以来、Ted は SharePoint 2007 テクノロジに関するプロフェッショナルな開発者の教育に専念してきました。 テッドは、ビジネス ソリューションを構築するための開発プラットフォームとして SharePoint を使用する方法に焦点を当てた「Windows SharePoint サービス内 3.0」というタイトルのマイクロソフト プレスの本を書き終えました。 また、MSDN マガジンの開発者向けのコラム「オフィススペース」も執筆しています。
