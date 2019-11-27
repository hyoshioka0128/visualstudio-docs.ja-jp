---
title: DSL | の MSI および VSIX のデプロイMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4917fc81f439ef0185a753fb1c4c85e460eb7681
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297744"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL の MSI および VSIX 配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドメイン固有言語は、自分のコンピューターまたは他のコンピューターにインストールできます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、ターゲットコンピューターに既にインストールされている必要があります。

## <a name="which"></a>VSIX と MSI の展開の選択
 ドメイン固有言語を展開するには、次の2つの方法があります。

|メソッド|メリット|
|------------|--------------|
|VSX ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能)|デプロイが非常に簡単: DslPackage プロジェクトから **.vsix**ファイルをコピーして実行します。<br /><br /> 詳細について[は、「VSX を使用した DSL のインストールとアンインストール](#Installing)」を参照してください。|
|MSI (インストーラーファイル)|-ユーザーが DSL ファイルをダブルクリックして [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を開けるようにします。<br />-ターゲットコンピューターの DSL ファイルの種類にアイコンを関連付けます。<br />-XSD (XML スキーマ) を DSL ファイルの種類に関連付けます。 これにより、ファイルが [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]に読み込まれるときに警告が回避されます。<br /><br /> MSI を作成するには、ソリューションにセットアッププロジェクトを追加する必要があります。<br /><br /> 詳細については、「 [MSI ファイルを使用した DSL の展開](#msi)」を参照してください。|

## <a name="Installing"></a>VSX を使用して DSL をインストールおよびアンインストールする
 DSL がこの方法でインストールされている場合、ユーザーは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]内から DSL ファイルを開くことができますが、Windows エクスプローラーからファイルを開くことはできません。

#### <a name="to-install-a-dsl-by-using-the-vsx"></a>VSX を使用して DSL をインストールするには

1. コンピューターで、DSL パッケージプロジェクトによって作成された **.vsix**ファイルを見つけます。

    1. **ソリューションエクスプローラー**で、 **[dslpackage]** プロジェクトを右クリックし、 **[エクスプローラーでフォルダーを開く]** をクリックします。

    2. _YourProject_ **\\\*\\** ファイルの bin を見つけ**ます。DslPackage。 .vsix**

2. DSL をインストールするターゲットコンピューターに .vsix ファイルをコピー**します。** 自分のコンピューターでも別のコンピューターでもかまいません。

    - ターゲットコンピューターは、実行時に Dsl をサポートする [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] のいずれかのエディションを搭載している必要があります。 詳細については、「[サポートされている Visual Studio エディションの視覚化 & モデリング SDK](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)」を参照してください。

    - 対象のコンピューターには、 **DslPackage\source.extensions.manifest**で指定された [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のいずれかのエディションが必要です。

3. ターゲットコンピューターで、 **.vsix**ファイルをダブルクリックします。

     **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。

4. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]を起動または再起動します。

5. DSL をテストするには、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用して、DSL 用に定義した拡張子を持つ新しいファイルを作成します。

#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>VSX を使用してインストールされた DSL をアンインストールするには

1. **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

2. **[インストール済みの拡張機能]** を展開します。

3. DSL が定義されている拡張機能を選択し、 **[アンインストール]** をクリックします。

   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 その場合は、以下の場所からファイルを削除して、拡張機能を削除します。

   *Localappdata* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="msi"></a>MSI で DSL を展開する
 DSL 用の MSI (Windows インストーラー) ファイルを定義することで、ユーザーが Windows エクスプローラーから DSL ファイルを開けるようにすることができます。 また、アイコンと短い説明をファイル名の拡張子に関連付けることもできます。 また、MSI では、DSL ファイルの検証に使用できる XSD をインストールできます。 必要に応じて、同時にインストールされる他のコンポーネントを MSI に追加することができます。

 MSI ファイルおよびその他の展開オプションの詳細については、「[アプリケーション、サービス、およびコンポーネントの展開](../deployment/deploying-applications-services-and-components.md)」を参照してください。

 MSI をビルドするには、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションにセットアッププロジェクトを追加します。 セットアッププロジェクトを作成する最も簡単な方法は、CreateMsiSetupProject.tt テンプレートを使用することです。このテンプレートは、 [Vmsdk サイト](https://go.microsoft.com/fwlink/?LinkID=186128)からダウンロードできます。

#### <a name="to-deploy-a-dsl-in-an-msi"></a>DSL を MSI に展開するには

1. 拡張機能マニフェストで `InstalledByMsi` を設定します。 これにより、MSI 以外で VSX をインストールおよびアンインストールすることができなくなります。 MSI に他のコンポーネントを含める場合は、これが重要です。

   1. DslPackage\source.extension.tt を開く

   2. `<SupportedProducts>`する前に、次の行を挿入します。

       ```
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. Windows エクスプローラーで DSL を表すアイコンを作成または編集します。 たとえば、 **DslPackage\Resources\File.ico**を編集します。

3. DSL の次の属性が正しいことを確認します。

   - DSL エクスプローラーでルートノードをクリックし、プロパティウィンドウで次の内容を確認します。

       - 説明

       - バージョン

   - **[エディター]** ノードをクリックし、プロパティウィンドウの **[アイコン]** をクリックします。 **Dslpackage\ Resources**でアイコンファイルを参照するように値を設定し**ます。たとえば、ファイル .ico などです。**

   - **[ビルド]** メニューの **[Configuration Manager]** を開き、 **[リリース]** や **[デバッグ]** など、ビルドする構成を選択します。

4. [視覚化とモデリング SDK のホームページ](https://go.microsoft.com/fwlink/?LinkID=186128)にアクセスし、 **[ダウンロード]** タブから**CreateMsiSetupProject.tt**をダウンロードします。

5. Dsl プロジェクトに**CreateMsiSetupProject.tt**を追加します。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によって、CreateMsiSetupProject という名前のファイルが作成されます。 **.vdproj**です。

6. Windows エクスプローラーで、Dsl\\*. .vdproj を Setup という名前の新しいフォルダーにコピーします。

    (必要に応じて、Dsl プロジェクトから CreateMsiSetupProject.tt を除外できるようになりました)。

7. **ソリューションエクスプローラー**で、既存のプロジェクトとして**セットアップ\\\*.vdproj**を追加します。

8. **[プロジェクト]** メニューの **[プロジェクトの依存関係]** をクリックします。

    **[プロジェクトの依存関係]** ダイアログボックスで、セットアッププロジェクトを選択します。

    **[Dslpackage]** の横にあるチェックボックスをオンにします。

9. ソリューションをリビルドします。

10. Windows エクスプローラーで、セットアッププロジェクトでビルドされた MSI ファイルを見つけます。

     DSL をインストールするコンピューターに MSI ファイルをコピーします。 MSI ファイルをダブルクリックします。 インストーラーを実行します。

11. ターゲットコンピューターで、DSL のファイル拡張子を持つ新しいファイルを作成します。 次のことを確認します。

    - Windows エクスプローラーのリストビューでは、定義したアイコンと説明がファイルに表示されます。

    - ファイルをダブルクリックすると [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が起動し、dsl エディターで DSL ファイルが開きます。

    必要に応じて、テキストテンプレートを使用する代わりに、手動でセットアッププロジェクトを作成することもできます。 この手順を含むチュートリアルについては、[視覚化とモデリング SDK ラボ](https://go.microsoft.com/fwlink/?LinkId=208878)の第5章を参照してください。

#### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>MSI からインストールされた DSL をアンインストールするには

1. Windows で、コントロールパネルの **[プログラムと機能]** を開きます。

2. DSL をアンインストールします。

3. Visual Studio を再起動します。
