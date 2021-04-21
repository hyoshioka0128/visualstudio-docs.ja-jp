---
title: ClickOnce を使用して Office ソリューションを配置する
description: ClickOnce を使用する場合に、より少数の手順で Office ソリューションを配置する方法について説明します。 更新プログラムを発行する場合は、ソリューションはそれらを自動的に検出してインストールします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, deploying solutions
- ClickOnce deployment [Office development in Visual Studio], deploying solutions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 03b4f3d2f1a342f6c1977d616793634500850e7a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828619"
---
# <a name="deploy-an-office-solution-by-using-clickonce"></a>ClickOnce を使用して Office ソリューションを配置する
  ClickOnce を使用する場合は、少しの手順で Office ソリューションを配置できます。 更新プログラムを発行する場合は、ソリューションはそれらを自動的に検出してインストールします。 ただし、ClickOnce を使用する場合は、コンピューターのユーザーごとに、ソリューションを個別にインストールする必要があります。 そのため、複数のユーザーが同じコンピューターでソリューションを実行する場合は、Windows インストーラー (*.msi*) の使用を検討する必要があります。

## <a name="in-this-topic"></a>このトピックの内容

- [ソリューションの発行](#Publish)

- [ソリューションに信頼を付与する方法の決定](#Trust)

- [ユーザーによるソリューションのインストールの支援](#Helping)

- [ソリューションのドキュメントをエンド ユーザーのコンピューターに配置 (ドキュメント レベルのカスタマイズのみ)](#Put)

- [ソリューションのドキュメントを、SharePoint を実行しているサーバーに配置 (ドキュメント レベルのカスタマイズのみ)](#SharePoint)

- [カスタムインストーラーを作成する](#Custom)

- [更新プログラムの発行](#Update)

- [ソリューションのインストール場所の変更](#Location)

- [ソリューションを以前のバージョンにロールバック](#Roll)

  Windows インストーラーファイルを作成して Office ソリューションを配置する方法の詳細については、「 [Windows インストーラーを使用した office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="publish-the-solution"></a><a name="Publish"></a> ソリューションを発行する
 ソリューションを発行するには、 **発行ウィザード** または **プロジェクトデザイナー** を使用します。 この手順では、 **プロジェクトデザイナー** を使用します。これは、発行オプションの完全なセットを提供するためです。 「 [Visual Studio&#41;での Office 開発 &#40;の発行ウィザード」を ](../vsto/publish-wizard-office-development-in-visual-studio.md)参照してください。

#### <a name="to-publish-the-solution"></a>ソリューションを発行するには

1. **ソリューションエクスプローラー** で、プロジェクトの名前が付けられているノードを選択します。

2. メニュー バーで、 **[プロジェクト]**、[ *ProjectName* **のプロパティ]**」を参照してください。

3. **プロジェクトデザイナー** で、[**発行**] タブを選択します。次の図が示されています。

    ![プロジェクト デザイナーの [発行] タブ](../vsto/media/vsto-publishtab.png "プロジェクト デザイナーの [発行] タブ")

4. [ **発行フォルダーの場所 (ftp サーバーまたはファイルパス)** ] ボックスに、 **プロジェクトデザイナー** でソリューションファイルをコピーするフォルダーのパスを入力します。

    次のいずれかの種類のパスを入力できます。

   - ローカルパス (たとえば、 *C:\FolderName\FolderName*)。

   - ネットワーク上のフォルダーへの汎用名前付け規則 (UNC) パス (たとえば、 *\\ \ServerName\FolderName*)。

   - 相対パス (たとえば、プロジェクトが既定で発行されるフォルダーである *Publishfolder \\* など)。

5. [ **インストールフォルダーの URL** ] ボックスに、エンドユーザーがソリューションを検索する場所の完全修飾パスを入力します。

    まだ場所がわからない場合は、このフィールドに何も入力しないでください。 既定では、ClickOnce はこのフォルダーの中で、ユーザーがソリューションをインストールするための更新プログラムを検索します。

6. **[必須コンポーネント]** ボタンをクリックします。

7. [ **必須** コンポーネント] ダイアログボックスで、[ **必須コンポーネントをインストールするためのセットアッププログラムを作成する** ] チェックボックスがオンになっていることを確認します。

8. [ **インストールする必須コンポーネントの選択** ] ボックスの一覧で、 **Windows インストーラー 4.5** と適切な .NET Framework パッケージのチェックボックスをオンにします。

    たとえば、ソリューションでを対象としている場合は、 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] **Windows インストーラー 4.5** のチェックボックスをオンにし、 **Microsoft .NET Framework 4.5 Full** を選択します。

9. ソリューションが .NET Framework 4.5 を対象としている場合は、[ **Visual Studio 2010 Tools For Office Runtime** ] チェックボックスもオンにします。

    > [!NOTE]
    > 既定では、このチェックボックスは表示されません。 このチェック ボックスを表示するには、ブートストラップ パッケージを作成する必要があります。 「 [Visual Studio 2012 を使用した Office 2013 VSTO アドインのブートストラップパッケージの作成](create-vsto-add-ins-for-office-by-using-visual-studio.md)」を参照してください。

10. [ **必須コンポーネントのインストール場所の指定**] で、表示されるオプションの1つを選択し、[ **OK** ] をクリックします。

     各オプションの説明を次の表に示します。

    |オプション|説明|
    |------------|-----------------|
    |**必須コンポーネントをコンポーネントの開発元の Web サイトからダウンロードする**|ユーザーは、販売元からこれらの必須コンポーネントをダウンロードしてインストールするように求められます。|
    |**アプリケーションと同じ場所から必須コンポーネントをダウンロードする**|必要なソフトウェアは、ソリューションと共にインストールされます。 このオプションを選択すると、Visual Studio はすべての必須パッケージを発行場所に自動的にコピーします。 このオプションを使用するには、必須パッケージが開発用コンピューターに存在する必要があります。|
    |**次の場所から必須コンポーネントをダウンロード**|Visual Studio は、指定した場所にすべての必須パッケージをコピーし、ソリューションと共にそれらをインストールします。|

     「 [[必須コンポーネント] ダイアログボックス](../ide/reference/prerequisites-dialog-box.md)」を参照してください。

11. [ **更新プログラム** ] ボタンをクリックし、各エンドユーザーの VSTO アドインまたはカスタマイズで更新プログラムを確認する頻度を指定して、[ **OK** ] をクリックします。

    > [!NOTE]
    > CD またはリムーバブルドライブを使用してを展開する場合は、[ **更新プログラムを確認しない** ] オプションボタンを選択します。

     更新プログラムを発行する方法の詳細については、「 [更新プログラムの発行](#Update)」を参照してください。

12. [ **オプション** ] ボタンをクリックし、[ **オプション** ] ダイアログボックスのオプションを確認して、[ **OK** ] をクリックします。

13. [ **今すぐ発行** ] ボタンをクリックします。

     この手順で既に指定した発行フォルダーに、Visual Studio は次のフォルダーとファイルを追加します。

    - **アプリケーションファイル** フォルダー。

    - セットアップ プログラム。

    - 最新バージョンの配置マニフェストを指す配置マニフェスト。

      **Application Files** フォルダーには、発行する各バージョンのサブフォルダーが含まれています。 バージョン固有の各サブフォルダーには、次のファイルが含まれます。

    - アプリケーション マニフェスト。

    - 配置マニフェスト。

    - カスタマイズ アセンブリ。

      次の図に、Outlook VSTO アドインに対応する発行フォルダーの構造を示します。

      ![フォルダー構造の発行](../vsto/media/publishfolderstructure.png "発行フォルダーの構造")

    > [!NOTE]
    > ClickOnce はアセンブリに .deploy 拡張子を追加し *ます。* これにより、安全にインストールされたインターネットインフォメーションサービス (IIS) が安全でない拡張機能のためにファイルをブロックしなくなります。 ユーザーがソリューションをインストールすると、ClickOnce によって *.deploy* 拡張子が削除されます。

14. この手順で既に指定したインストール場所に、ソリューション ファイルをコピーします。

## <a name="decide-how-you-want-to-grant-trust-to-the-solution"></a><a name="Trust"></a> ソリューションに信頼を付与する方法を決定する
 ユーザーのコンピューターでソリューションを実行する前に、次のいずれかの方法で信頼を付与する必要があります。そうしない場合は、ユーザーはソリューションをインストールするときに、信頼プロンプトに応答する必要が生じます。 ソリューションに信頼を付与するには、既知の信頼される発行者を特定する証明書を使用してマニフェストに署名します。 「 [アプリケーションマニフェストと配置マニフェストに署名することによるソリューションの信頼](../vsto/granting-trust-to-office-solutions.md#Signing)」を参照してください。

 ドキュメントレベルのカスタマイズを配置し、ドキュメントをユーザーのコンピューター上のフォルダーに配置する場合、またはドキュメントを SharePoint サイトで使用できるようにする場合は、Office がドキュメントの場所を信頼していることを確認します。 「 [ドキュメントへの信頼の付与」を](../vsto/granting-trust-to-documents.md)参照してください。

## <a name="help-users-install-the-solution"></a><a name="Helping"></a> ユーザーがソリューションをインストールできるようにする
 ユーザーは、セットアッププログラムを実行するか、配置マニフェストを開くか、ドキュメントレベルのカスタマイズ中にドキュメントを直接開くことで、ソリューションをインストールできます。 ベスト プラクティスとして、ユーザーはセットアップ プログラムを使用してソリューションをインストールする必要があります。 他の2つの方法では、前提条件となるソフトウェアがインストールされていることを確認できません。 ユーザーがインストール場所からドキュメントを開こうとする場合は、Office アプリケーションのセキュリティ センターにある信頼できる場所の一覧に、そのインストール場所を追加する必要があります。

### <a name="opening-the-document-of-a-document-level-customization"></a>ドキュメント レベルのカスタマイズに対応するドキュメントを開く
 ドキュメント レベルのカスタマイズに対応するドキュメントの場合は、ユーザーはインストール場所からそのドキュメントを直接開くか、またはドキュメントをローカル コンピューターにコピーしてからコピー先ドキュメントを開くことができます。

 ベスト プラクティスとして、ユーザーはローカル コンピューター上にあるドキュメントのコピーを開く必要があります。その結果、複数のユーザーが同じドキュメントを同時に開こうとすることはありません。 このプラクティスを強制するために、ユーザーのコンピューターにドキュメントをコピーするようにセットアップ プログラムを構成することができます。 「 [ソリューションのドキュメントをエンドユーザーのコンピューターに配置する (ドキュメントレベルのカスタマイズのみ)](#Put)」を参照してください。

### <a name="install-the-solution-by-opening-the-deployment-manifest-from-an-iis-website"></a>IIS web サイトから配置マニフェストを開き、ソリューションをインストールします。
 ユーザーは、Web で配置マニフェストを開くことにより、Office ソリューションをインストールできます。 ただし、インターネットインフォメーションサービス (IIS) のセキュリティで保護されたインストールでは、拡張子が *.vsto* のファイルはブロックされます。 IIS を使用して Office ソリューションを配置する前に、IIS に MIME の種類を定義する必要があります。

##### <a name="to-add-the-vsto-mime-type-to-iis-60"></a>IIS 6.0 に MIME の種類 (.vsto) を追加するには

1. Iis 6.0 を実行しているサーバーで、[**スタート**] [  >  **すべてのプログラム**] [  >  **管理ツール**] [  >   **インターネットインフォメーションサービス (iis) マネージャー**] の順に選択します。

2. 構成しているコンピューター名、 **Web サイト** フォルダー、または web サイトを選択します。

3. メニューバーで [**アクション** のプロパティ] を選択し  >  ます。

4. [ **HTTP ヘッダー** ] タブで、[ **MIME の種類** ] ボタンをクリックします。

5. [ **MIME の種類** ] ウィンドウで、[ **新規作成** ] をクリックします。

6. [ **Mime の種類** ] ウィンドウで、拡張子として「 **.vsto** 」と入力し、mime の種類として「 **application/x-ms-vsto** 」と入力して、新しい設定を適用します。

    > [!NOTE]
    > 変更を有効にするために、World Wide Web 発行サービスを再起動するか、ワーカー プロセスがリサイクルされるまで待つ必要があります。 その後、ブラウザーのディスクキャッシュをフラッシュしてから、 *.vsto* ファイルをもう一度開く必要があります。

##### <a name="to-add-the-vsto-mime-type-to-iis-70"></a>IIS 7.0 に MIME の種類 (.vsto) を追加するには

1. IIS 7.0 を実行しているサーバーで、[**スタート**] [すべてのプログラム] [アクセサリ] の順に選択し  >    >  ます。

2. [**コマンドプロンプト**] のショートカットメニューを開き、[**管理者として実行**] を選択します。

3. [ **名前** ] ボックスに次のパスを入力し、[ **OK** ] をクリックします。

    ```cmd
    %windir%\system32\inetsrv
    ```

4. 次のコマンドを入力し、新しい設定を適用します。

    ```cmd
    set config /section:staticContent /+[fileExtension='.vsto',mimeType='application/x-ms-vsto']
    ```

    > [!NOTE]
    > 変更を有効にするために、World Wide Web Publishing Service を再起動するか、ワーカー プロセスがリサイクルされるまで待つ必要があります。 その後、ブラウザーのディスクキャッシュをフラッシュしてから、 *.vsto* ファイルをもう一度開く必要があります。

## <a name="put-the-document-of-a-solution-onto-the-end-users-computer-document-level-customizations-only"></a><a name="Put"></a> ソリューションのドキュメントをエンドユーザーのコンピューターに配置する (ドキュメントレベルのカスタマイズのみ)
 配置後アクションを作成することによって、ソリューションのドキュメントをエンドユーザーのコンピューターにコピーできます。 そうすることで、ユーザーはソリューションをインストールした後で、インストール場所からコンピューターにドキュメントを手動でコピーする必要がなくなります。 配置後アクションを定義するクラスを作成し、ソリューションをビルドして発行し、アプリケーションマニフェストを変更して、アプリケーションマニフェストと配置マニフェストに再署名する必要があります。

 次の手順では、プロジェクト名が **Excelworkbook** であることを前提としています。また、このソリューションは、コンピューター上に **c:\ publish** という名前の作成されたフォルダーに発行する必要があります。

### <a name="create-a-class-that-defines-the-post-deployment-action"></a>配置後アクションを定義するクラスを作成します。

1. メニューバーで、[**ファイル**] [  >    >  **新しいプロジェクト** の追加] の順に選択します。

2. [ **新しいプロジェクトの追加** ] ダイアログボックスの [ **インストールされたテンプレート** ] ペインで、[ **Windows** ] フォルダーを選択します。

3. [ **テンプレート** ] ペインで、[ **クラスライブラリ** ] テンプレートを選択します。

4. [ **名前** ] フィールドに「 **FileCopyPDA**」と入力し、[ **OK** ] をクリックします。

5. **ソリューションエクスプローラー** で、 **FileCopyPDA** プロジェクトを選択します。

6. メニュー バーで、 **[プロジェクト]**  >  **[参照の追加]** の順に選択します。

7. [ **.Net** ] タブで、およびへの参照を追加し `Microsoft.VisualStudio.Tools.Applications.Runtime` `Microsoft.VisualStudio.Tools.Applications.ServerDocument` ます。

8. クラスの名前を `FileCopyPDA` に変更してから、ファイルの内容を次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - ドキュメントをユーザーのデスクトップにコピーします。

   - _AssemblyLocation プロパティを相対パスから配置マニフェストの完全修飾パスに変更します。

   - ユーザーがソリューションをアンインストールする場合は、ファイルを削除します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookpda/filecopypda/class1.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookpda/filecopypda/class1.cs" id="Snippet7":::

### <a name="build-and-publish-the-solution"></a>ソリューションをビルドし、発行します。

1. **ソリューションエクスプローラー** で、 **FileCopyPDA** プロジェクトのショートカットメニューを開き、[**ビルド**] を選択します。

2. **Excelworkbook** プロジェクトのショートカットメニューを開き、[**ビルド**] を選択します。

3. **Excelworkbook** プロジェクトのショートカットメニューを開き、[参照の **追加**] を選択します。

4. [ **参照の追加** ] ダイアログボックスで、[ **プロジェクト** ] タブを選択し、[ **FileCopyPDA**] を選択して、[ **OK** ] をクリックします。

5. **ソリューションエクスプローラー** で、 **excelworkbook** プロジェクトを選択します。

6. メニューバーで、[**プロジェクト**] [新しいフォルダー] の順に選択し  >  ます。

7. **データ** を入力し、 **enter** キーを押します。

8. **ソリューションエクスプローラー** で、[**データ**] フォルダーを選択します。

9. メニューバーで、[**プロジェクト**] [既存の項目の追加] の順に選択し  >  ます。

10. [ **既存項目の追加** ] ダイアログボックスで、 **excelworkbook** プロジェクトの出力ディレクトリを参照し、 **ExcelWorkbook.xlsx** ファイルを選択して、[ **追加** ] ボタンをクリックします。

11. **ソリューションエクスプローラー** **ExcelWorkbook.xlsx** ファイルを選択します。

12. [ **プロパティ** ] ウィンドウで、[ **ビルドアクション** ] プロパティを [ **コンテンツ** ] に、[ **出力ディレクトリにコピー** ] プロパティを [ **新しい場合はコピー** する] に変更します。

     これらの手順を完了すると、プロジェクトは次の図のようになります。

     ![配置後アクションのプロジェクト構造。](../vsto/media/vsto-postdeployment.png "配置後アクションのプロジェクト構造。")

13. **Excelworkbook** プロジェクトを発行します。

### <a name="modify-the-application-manifest"></a>アプリケーション マニフェストの変更

1. **エクスプローラー** を使用して、ソリューションディレクトリ **c:\ publish** を開きます。

2. [ **アプリケーションファイル** ] フォルダーを開き、ソリューションの最新の発行バージョンに対応するフォルダーを開きます。

3. メモ帳などのテキストエディターで **ExcelWorkbook.dll マニフェスト** ファイルを開きます。

4. `</vstav3:update>` 要素の後に、次のコードを追加します。 要素の class 属性には、 `<vstav3:entryPoint>` 次の構文を使用します: *NamespaceName*。 次の例では、名前空間名とクラス名は同じであるため、最終的にエントリ ポイント名は `FileCopyPDA.FileCopyPDA` になります。

    ```xml
    <vstav3:postActions>
      <vstav3:postAction>
        <vstav3:entryPoint
          class="FileCopyPDA.FileCopyPDA">
          <assemblyIdentity
            name="FileCopyPDA"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
        <vstav3:postActionData>
        </vstav3:postActionData>
      </vstav3:postAction>
    </vstav3:postActions>
    ```

### <a name="re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストへの再署名

1. **%USERPROFILE%\Documents\Visual Studio 2013 \ Projects\ExcelWorkbook\ExcelWorkbook** フォルダーで、 **ExcelWorkbook_TemporaryKey .pfx** 証明書ファイルをコピーし、 *publishfolder* **\Application Files\ExcelWorkbook** \_ _MostRecentPublishedVersion_ フォルダーに貼り付けます。

2. Visual Studio コマンドプロンプトを開き、ディレクトリを **c:\publish\Application Files\ExcelWorkbook** \_ _MostRecentPublishedVersion_ フォルダー (たとえば **c:\publish\Application Files \ ExcelWorkbook_1_0_0_4**) に変更します。

3. 次のコマンドを実行し、変更したアプリケーション マニフェストに署名します。

    ```cmd
    mage -sign ExcelWorkbook.dll.manifest -certfile ExcelWorkbook_TemporaryKey.pfx
    ```

     "ExcelWorkbook.dll.manifest が正常に署名されました" というメッセージが表示されます。

4. 次のコマンドを実行して、 **c:\ publish** フォルダーに移動し、デプロイマニフェストを更新して署名します。

    ```cmd
    mage -update ExcelWorkbook.vsto -appmanifest "Application Files\Ex
    celWorkbookMostRecentVersionNumber>\ExcelWorkbook.dll.manifest" -certfile "Application Files\ExcelWorkbookMostRecentVersionNumber>\ExcelWorkbook_TemporaryKey.pfx"
    ```

    > [!NOTE]
    > 前の例では、MostRecentVersionNumber を、ソリューションの最後に発行されたバージョンのバージョン番号 ( **1_0_0_4** など) に置き換えます。

     "ExcelWorkbook.vsto 正常に署名されました" というメッセージが表示されます。

5. *Excelworkbook の .vsto* ファイルを **c:\publish\Application Files\ExcelWorkbook** \_ _MostRecentVersionNumber_ ディレクトリにコピーします。

## <a name="put-the-document-of-a-solution-onto-a-server-thats-running-sharepoint-document-level-customizations-only"></a><a name="SharePoint"></a> SharePoint を実行しているサーバーにソリューションのドキュメントを配置する (ドキュメントレベルのカスタマイズのみ)
 SharePoint を使用して、エンド ユーザーに対してドキュメント レベルのカスタマイズを発行できます。 ユーザーが SharePoint サイトにアクセスし、ドキュメントを開くと、ランタイムが自動的に共有ネットワーク フォルダーからユーザーのローカル コンピューターにソリューションをインストールします。 ソリューションをローカル インストールした後、ドキュメントをデスクトップなど別の場所にコピーした場合でも、カスタマイズは引き続き機能します。

#### <a name="to-put-the-document-on-a-server-thats-running-sharepoint"></a>SharePoint を実行しているサーバーにドキュメントを配置するには

1. SharePoint サイト上のドキュメント ライブラリにソリューション ドキュメントを追加します。

2. 次の方法のいずれかに対応する手順を実行します。

    - Office 構成ツールを使用し、すべてのユーザーのコンピューターで Word または Excel のセキュリティ センターに、SharePoint を実行しているサーバーを追加します。

         「 [セキュリティポリシーと Office 2010 の設定」を](/previous-versions/office/office-2010/cc178946(v=office.14))参照してください。

    - 各ユーザーが確実に次の手順を実行するようにします。

        1. ローカルコンピューターで Word または Excel を開き、[ **ファイル** ] タブを選択し、[ **オプション** ] ボタンをクリックします。

        2. [ **セキュリティセンター** ] ダイアログボックスで、[ **信頼できる場所** ] ボタンをクリックします。

        3. [ **ネットワーク上の信頼できる場所を許可する (推奨しません)** ] チェックボックスをオンにし、[ **新しい場所の追加** ] をクリックします。

        4. [ **パス** ] ボックスに、アップロードしたドキュメントを含む SharePoint ドキュメントライブラリの URL (など) を入力し *http://SharePointServerName/TeamName/ProjectName/DocumentLibraryName* ます。

             既定の Web ページの名前 ( *default.aspx* や *AllItems* など) は追加しないでください。

        5. [ **この場所のサブフォルダーも信頼** する] チェックボックスをオンにし、[ **OK** ] をクリックします。

             ユーザーが SharePoint サイトからドキュメントを開いた時点で、そのドキュメントが開かれ、カスタマイズがインストールされます。 ユーザーは、ドキュメントを自分のデスクトップにコピーすることができます。 ドキュメント内のプロパティは、ドキュメントが存在しているネットワークの場所を指しているので、カスタマイズは引き続き実行されます。

## <a name="create-a-custom-installer"></a><a name="Custom"></a> カスタムインストーラーを作成する
 ソリューションの発行時に作成されたセットアッププログラムを使用する代わりに、Office ソリューションのカスタムインストーラーを作成できます。 たとえば、サインインスクリプトを使用してインストールを開始したり、バッチファイルを使用してユーザーの操作なしでソリューションをインストールしたりすることができます。 このようなシナリオは、エンド ユーザーのコンピューターに必須コンポーネントがインストール済みの場合に最適です。

 カスタムインストールプロセスの一部として、次の場所に既定でインストールされる Office ソリューション (*VSTOInstaller.exe*) 用のインストーラーツールを呼び出します。

 *%commonprogramfiles%\microsoft shared\VSTO\10.0\VSTOInstaller.exe*

 ツールがその場所にない場合は、 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSTO Runtime Setup\v4\InstallerPath** または **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSTO Runtime Setup\v4\InstallerPath** レジストリキーを使用して、そのツールへのパスを見つけることができます。

 *VSTOinstaller.exe* では、次のパラメーターを使用できます。

| パラメーター | 定義 |
|------------------| - |
| /Install または /I | ソリューションをインストールします。 このオプションの後に配置マニフェストのパスを指定する必要があります。 ローカル コンピューター上のパス、汎用名前付けの規則 (UNC) のファイル共有を指定できます。 ローカルパス (*C:\FolderName\PublishFolder*)、相対パス (*\\ 発行*)、または完全修飾の場所 (*\\ \ServerName\FolderName* または http://<em>ServerName/FolderName</em>) を指定できます。 |
| /Uninstall または /U | ソリューションをアンインストールします。 このオプションの後に配置マニフェストのパスを指定する必要があります。 ローカル コンピューター上のパス、UNC ファイル共有を指定できます。 ローカルパス (*c:\FolderName\PublishFolder*)、相対パス (*\\ 発行*)、または完全修飾の場所 (*\\ \ServerName\FolderName* または http://<em>ServerName/FolderName</em>) を指定できます。 |
| /Silent または /S | ユーザーに入力を要求したりメッセージを表示したりすることなくソリューションをインストールまたはアンインストールします。 信頼プロンプトが必要な場合、カスタマイズはインストールまたは更新されません。 |
| /Help または /? | ヘルプ情報を表示します。 |

 *VSTOinstaller.exe* を実行すると、次のエラーコードが表示される場合があります。

|エラー コード|定義|
|----------------|----------------|
|0|ソリューションが正常にインストールまたはアンインストールされたか、VSTOInstaller ヘルプが表示されました。|
|-100|1つ以上のコマンドラインオプションが無効であるか、または複数回設定されました。 詳細については、「vstoinstaller/?」と入力してください。 または、「 [ClickOnce Office ソリューションのカスタムインストーラーを作成する](/previous-versions/bb772078(v=vs.110))」を参照してください。|
|-101|1つ以上のコマンドラインオプションが無効です。 詳細については、"vstoinstaller /?" と入力してください。|
|-200|配置マニフェストの URI が無効です。 詳細については、"vstoinstaller /?" と入力してください。|
|-201|配置マニフェストが有効ではないため、ソリューションをインストールできませんでした。 「 [Office ソリューションの配置マニフェスト」を](../vsto/deployment-manifests-for-office-solutions.md)参照してください。|
|-202|アプリケーションマニフェストの Visual Studio Tools for Office セクションが有効ではないため、ソリューションをインストールできませんでした。 「 [Office ソリューションのアプリケーションマニフェスト」を](../vsto/application-manifests-for-office-solutions.md)参照してください。|
|-203|ダウンロードエラーが発生したため、ソリューションをインストールできませんでした。 配置マニフェストの URI またはネットワーク ファイルの位置を確認し、もう一度、実行してみてください。|
|-300|セキュリティ例外が発生したため、ソリューションをインストールできませんでした。 「 [Office ソリューションのセキュリティ保護](../vsto/securing-office-solutions.md)」を参照してください。|
|-400|ソリューションをインストールできませんでした。|
|-401|ソリューションをアンインストールできませんでした。|
|-500|ソリューションをインストールまたはアンインストールできなかったこと、または配置マニフェストをダウンロードできなかったことが原因で、操作は取り消されました。|

## <a name="publish-an-update"></a><a name="Update"></a> 更新プログラムの発行
 ソリューションを更新するには、 **プロジェクトデザイナー** または **発行ウィザード** を使用してもう一度発行し、更新したソリューションをインストール場所にコピーします。 インストール場所にファイルをコピーするときに、前のファイルを確実に上書きしてください。

 次回ソリューションが更新プログラムを確認するときに、新しいバージョンが自動的に検出され、読み込まれます。

## <a name="change-the-installation-location-of-a-solution"></a><a name="Location"></a> ソリューションのインストール場所の変更
 ソリューションを発行した後、インストール パスの追加または変更を行うことができます。 次の理由の 1 つ以上により、インストール パスを変更する可能性があります:

- インストール パスが既知になる前に、セットアップ プログラムをコンパイルした。

- ソリューション ファイルは、別の場所からコピーされたものである。

- インストール ファイルをホストするサーバーの名前または場所が変更された。

  ソリューションのインストール パスを変更するには、開発者がセットアップ プログラムを更新し、その後、ユーザーがそのプログラムを実行する必要があります。 ドキュメント レベルのカスタマイズの場合、新しい場所を指すように、ユーザーがドキュメントのプロパティを更新する必要もあります。

> [!NOTE]
> ドキュメントのプロパティを更新するようユーザーに要求しない場合は、更新されたドキュメントをインストール場所から取得するようにユーザーに依頼できます。

#### <a name="to-change-the-installation-path-in-the-setup-program"></a>セットアップ プログラムのインストール パスを変更するには

1. **コマンドプロンプト** ウィンドウを開き、ディレクトリをインストールフォルダーに変更します。

2. セットアップ プログラムを実行します。このとき、文字列として新しいインストール パスを表す `/url` パラメーターを指定します。

    次の例で、インストール パスを、Fabrikam の Web サイト上にある場所に変更する方法を示しますが、この URL は必要なパスに置き換えることができます。

   ```cmd
   setup.exe /url="http://www.fabrikam.com/newlocation"
   ```

   > [!NOTE]
   > 実行可能ファイルのシグネチャが無効化されることを示すメッセージが表示された場合は、ソリューションの署名に使用された証明書がもう有効ではなく、発行者が不明です。 その結果、ユーザーはソリューションをインストールする前に、ソリューションのソースを信頼することを示すために、メッセージを確認する必要があります。

   > [!NOTE]
   > URL の現在の値を表示するには、`setup.exe /url` を実行します。

   ドキュメントレベルのカスタマイズの場合、ユーザーはドキュメントを開き、その _AssemblyLocation プロパティを更新する必要があります。 次の手順では、ユーザーがこのタスクを実行する方法について説明します。

#### <a name="to-update-the-_assemblylocation-property-in-a-document"></a>ドキュメントの_AssemblyLocation プロパティを更新するには

1. [ **ファイル** ] タブで、次の図に示す [ **情報**] を選択します。

     ![Excel の [情報] タブ](../vsto/media/vsto-infotab.png "Excel の [情報] タブ")

2. 次の図に示すように、 **プロパティ** の一覧で [ **詳細プロパティ**] を選択します。

     ![Excel の [詳細プロパティ]。](../vsto/media/vsto-advanceddocumentproperties.png "Excel の [詳細プロパティ]。")

3. 次の図に示すように、[**プロパティ**] の一覧の [**カスタム**] タブで、[_AssemblyLocation] を選択します。

     ![[AssemblyLocation] プロパティ。](../vsto/media/vsto-assemblylocationproperty.png "[AssemblyLocation] プロパティ。")

     [ **値** ] ボックスには、配置マニフェストの識別子が表示されます。

4. 識別子の前に、*パス* | *識別子*(たとえば、 *File://ServerName/FolderName/FileName|74744e4b-e4d6-41eb-84f7-ad20346fe2d9*) にドキュメントの完全修飾パスを入力し、その後にバーを入力します。

     この識別子の形式を設定する方法の詳細については、「 [カスタムドキュメントプロパティの概要](../vsto/custom-document-properties-overview.md)」を参照してください。

5. [ **OK** ] ボタンをクリックし、ドキュメントを保存して閉じます。

6. セットアップ プログラムを実行します。このとき、指定の場所にあるソリューションをインストールするための /url パラメーターは指定しません。

## <a name="roll-back-a-solution-to-an-earlier-version"></a><a name="Roll"></a> ソリューションを以前のバージョンにロールバックする
 開発者がソリューションをロールバックすると、ユーザーはそのソリューションの以前のバージョンに戻されることになります。

#### <a name="to-roll-back-a-solution"></a>ソリューションをロールバックするには

1. ソリューションのインストール場所を開きます。

2. 最上位レベルの publish フォルダーで、配置マニフェスト ( *.vsto* ファイル) を削除します。

3. ロールバック先のバージョンに対応するサブフォルダーを見つけます。

4. このサブフォルダー内の配置マニフェストをトップレベルの発行フォルダーにコピーします。

     たとえば、 **outlookaddin1.dll** という名前のソリューションをバージョン1.0.0.1 からバージョン1.0.0.0 にロールバックするには、 **OutlookAddIn1_1_0_0_0** フォルダーから **outlookaddin1.dll** ファイルをコピーします。 最上位レベルの publish フォルダーにファイルを貼り付けて、既に存在していた **OutlookAddIn1_1_0_0_1** のバージョン固有の配置マニフェストを上書きします。

     次の図に、この例に対応する発行フォルダーの構造を示します。

     ![フォルダー構造の発行](../vsto/media/publishfolderstructure.png "発行フォルダーの構造")

     アプリケーションまたはカスタマイズされたドキュメントをユーザーが次回開くときに、配置マニフェストの変更が検出されます。 Office ソリューションの以前のバージョンは、ClickOnce キャッシュから実行されます。

> [!NOTE]
> ローカル データは、ソリューションの 1 つ前のバージョンについてのみ保存されます。 2つのバージョンをロールバックした場合、ローカルデータは保持されません。 ローカルデータの詳細については、「 [ClickOnce アプリケーションでローカルデータおよびリモートデータにアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
- [Office ソリューションの発行](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [方法: ClickOnce を使用して Office ソリューションを発行する](/previous-versions/bb386095(v=vs.110))
- [方法: ClickOnce Office ソリューションをインストールする](/previous-versions/bb608592(v=vs.110))
- [方法: ClickOnce を使用してドキュメントレベルの Office ソリューションを SharePoint サーバーに発行する](/previous-versions/bb608595(v=vs.110))
- [ClickOnce office ソリューションのカスタムインストーラーを作成する](/previous-versions/bb772078(v=vs.110))