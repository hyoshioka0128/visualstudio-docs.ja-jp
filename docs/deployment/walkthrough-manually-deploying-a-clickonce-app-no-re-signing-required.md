---
title: ClickOnce アプリを手動でデプロイして、ブランドを維持 &
description: 新しい配置マニフェストを生成せずに顧客のブランドを使用できる ClickOnce アプリケーションを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- branding
- preserved branding information
- ClickOnce deployment, manually
- multiple ClickOnce deployment and branding
- ClickOnce deployment, SDK tools
- customer deployments
- manual ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, deployed by others
ms.assetid: c21822fb-d4ee-42e4-b72d-41ee9786efe5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c0e8895f45524526fc8007ff909a9c541e9899b3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917259"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information"></a>チュートリアル: 再署名が不要でブランド情報を保持する ClickOnce アプリケーションを手動で配置する
アプリケーションを作成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] し、発行してデプロイするために顧客に提供する場合、従来はデプロイマニフェストを更新し、再署名する必要がありました。 ほとんどの場合、これは推奨される方法ですが、.NET Framework 3.5 では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 新しい配置マニフェストを再生成することなく、顧客がデプロイできるデプロイを作成することができます。 詳細については、「 [テストサーバーおよび運用サーバー用に ClickOnce アプリケーションを配置する](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)」を参照してください。

 アプリケーションを作成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] し、発行してデプロイするために顧客に提供すると、アプリケーションは顧客のブランドを使用したり、ブランドを保持したりすることができます。 たとえば、アプリケーションが1つの独自のアプリケーションである場合は、ブランド化を維持することができます。 お客様ごとにアプリケーションが高度にカスタマイズされている場合は、お客様のブランドを使用することをお勧めします。 .NET Framework 3.5 では、展開する組織にアプリケーションを提供するときに、ブランド、発行者情報、およびセキュリティ署名を保持できます。 詳細については、「 [他のユーザーが配置できるように ClickOnce アプリケーションを作成する](../deployment/creating-clickonce-applications-for-others-to-deploy.md)」を参照してください。

> [!NOTE]
> このチュートリアルでは、コマンドラインツール *Mage.exe* またはグラフィカルツール *MageUI.exe* を使用して、手動で展開を作成します。 手動配置の詳細については、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

## <a name="prerequisites"></a>前提条件
 このチュートリアルの手順を実行するには、次のものが必要です。

- デプロイの準備ができている Windows フォームアプリケーション。 このアプリケーションは *WindowsFormsApp1* と呼ばれます。

- Visual Studio または Windows SDK。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageexe"></a>Mage.exe を使用して複数のデプロイおよびブランドサポートを含む ClickOnce アプリケーションを配置するには

1. Visual Studio のコマンドプロンプトまたはコマンドプロンプトを開き、 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] ファイルを保存するディレクトリに移動し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

2. デプロイの現在のバージョンの後に、という名前のディレクトリを作成します。 アプリケーションを初めてデプロイする場合は、[ **1.0.0.0**] を選択します。

   > [!NOTE]
   > 配置のバージョンは、アプリケーションファイルのバージョンとは異なる場合があります。

3. **Bin** という名前のサブディレクトリを作成し、実行可能ファイル、アセンブリ、リソース、データファイルを含むすべてのアプリケーションファイルをここにコピーします。

4. Mage.exe の呼び出しを使用して、アプリケーションマニフェストを生成します。

   ```cmd
   mage -New Application -ToFile 1.0.0.0\WindowsFormsApp1.exe.manifest -Name "Windows Forms App 1" -Version 1.0.0.0 -FromDirectory 1.0.0.0\bin -UseManifestForTrust true -Publisher "A. Datum Corporation"
   ```

5. デジタル証明書を使用して、アプリケーションマニフェストに署名します。

   ```cmd
   mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx
   ```

6. *Mage.exe* の呼び出しを使用して、配置マニフェストを生成します。 既定では、 *Mage.exe* は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] インストール済みのアプリケーションとして展開をマークします。これにより、オンラインとオフラインの両方で実行できるようになります。 ユーザーがオンラインのときにのみアプリケーションを使用できるようにするには、 `-i` の値がである引数を使用し `f` ます。 このアプリケーションでは複数の配置機能を利用するため、 `-providerUrl` 引数を *Mage.exe* に除外します。 (バージョン3.5 より前の .NET Framework のバージョンでは、オフラインアプリケーションを除き、エラーが発生 `-providerUrl` します)。

   ```cmd
   mage -New Deployment -ToFile WindowsFormsApp1.application -Name "Windows Forms App 1" -Version 1.0.0.0 -AppManifest 1.0.0.0\WindowsFormsApp1.manifest
   ```

7. 配置マニフェストに署名しないでください。

8. すべてのファイルを顧客に提供します。ユーザーは、自分のネットワークにアプリケーションをデプロイします。

9. この時点で、顧客は自己生成された証明書を使用して配置マニフェストに署名する必要があります。 たとえば、Adventure Works という名前の会社に対して顧客が作業する場合、 *MakeCert.exe* ツールを使用して自己署名証明書を生成できます。 次に、 *Pvk2pfx.exe* ツールを使用して、 *MakeCert.exe* によって作成されたファイルを、 *Mage.exe* に渡すことができる PFX ファイルに結合します。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

10. 次に、この証明書を使用して配置マニフェストに署名します。

    ```cmd
    mage -Sign WindowsFormsApp1.application -CertFile MyCert.pfx
    ```

11. 顧客は、アプリケーションをユーザーに展開します。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageuiexe"></a>MageUI.exe を使用して複数のデプロイおよびブランドサポートを含む ClickOnce アプリケーションを配置するには

1. Visual Studio のコマンドプロンプトまたはコマンドプロンプトを開き、 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] ファイルを格納するディレクトリに移動し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

2. **Bin** という名前のサブディレクトリを作成し、実行可能ファイル、アセンブリ、リソース、データファイルを含むすべてのアプリケーションファイルをここにコピーします。

3. 現在のバージョンのデプロイの後に、という名前のサブディレクトリを作成します。 アプリケーションを初めてデプロイする場合は、[ **1.0.0.0**] を選択します。

   > [!NOTE]
   > 配置のバージョンは、アプリケーションファイルのバージョンとは異なる場合があります。

4. \\ **Bin** ディレクトリを、手順 2. で作成したディレクトリに移動します。

5. グラフィカルツール *MageUI.exe* を起動します。

   ```cmd
   MageUI.exe
   ```

6. メニューから [ **ファイル**]、[ **新規** 作成]、[ **アプリケーションマニフェスト** ] の順に選択して、新しいアプリケーションマニフェストを作成します。

7. [既定の **名前** ] タブで、この展開の名前とバージョン番号を入力します。 また、[ **発行元**] に値を指定します。この値は、アプリケーションの展開時に [スタート] メニューに表示される、アプリケーションのショートカットリンクのフォルダー名として使用されます。

8. [ **アプリケーションオプション** ] タブを選択し、[ **信頼情報にアプリケーションマニフェストを使用する**] をクリックします。 これにより、このアプリケーションのサードパーティブランドが有効になり [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

9. [**ファイル**] タブを選択し、[**アプリケーションディレクトリ**] テキストボックスの横にある [**参照**] ボタンをクリックします。

10. 手順 2. で作成したアプリケーションファイルが格納されているディレクトリを選択し、[フォルダーの選択] ダイアログボックスで [ **OK]** をクリックします。

11. [ **設定** ] ボタンをクリックして、すべてのアプリケーションファイルをファイルの一覧に追加します。 アプリケーションに複数の実行可能ファイルが含まれている場合は、[**ファイルの種類**] ドロップダウンリストから [**エントリポイント**] を選択して、この展開のメインの実行可能ファイルをスタートアップアプリケーションとしてマークします。 (アプリケーションに1つの実行可能ファイルしか含まれていない場合は、 *MageUI.exe* によってマークされます)。

12. [ **必要なアクセス許可** ] タブを選択し、アプリケーションでアサートする必要がある信頼のレベルを選択します。 既定値は **完全信頼** で、ほとんどのアプリケーションに適しています。

13. [ **ファイル**] メニューの [ **保存** ] をクリックし、アプリケーションマニフェストを保存します。 アプリケーションマニフェストの保存時に、署名を求めるメッセージが表示されます。

14. ファイルシステムにファイルとして保存されている証明書がある場合は、[ **証明書ファイルとして署名** する] オプションを使用して、省略記号ボタン ([.**.**.]) を使用してファイルシステムから証明書を選択します。

     \- または -

     コンピューターからアクセスできる証明書ストアに証明書が保存されている場合は、[ **保存された証明書で署名する] オプション** を選択し、表示された一覧から証明書を選択します。

15. メニューから [ **ファイル**]、[ **新規作成**]、[ **配置マニフェスト** ] を選択して配置マニフェストを作成します。次に、[ **名前** ] タブで、名前とバージョン番号 (この例では **1.0.0.0** ) を指定します。

16. [ **更新** ] タブに切り替えて、このアプリケーションを更新する頻度を指定します。 アプリケーションが配置 API を使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 更新プログラムを確認する場合は、[ **このアプリケーションで更新プログラムを確認** する] チェックボックスをオフにします。

17. [ **アプリケーション参照** ] タブに切り替えます。 **[マニフェストの選択** ] ボタンをクリックし、前の手順で作成したアプリケーションマニフェストを選択して、このタブのすべての値を事前設定できます。

18. [ **保存** ] を選択し、配置マニフェストをディスクに保存します。 アプリケーションマニフェストの保存時に、署名を求めるメッセージが表示されます。 署名せずにマニフェストを保存するには、[ **キャンセル** ] をクリックします。

19. すべてのアプリケーションファイルを顧客に提供します。

20. この時点で、顧客は自己生成された証明書を使用して配置マニフェストに署名する必要があります。 たとえば、Adventure Works という名前の会社に対して顧客が作業する場合、 *MakeCert.exe* ツールを使用して自己署名証明書を生成できます。 次に、 *Pvk2pfx.exe* ツールを使用して、 *MakeCert.exe* によって作成されたファイルを、 *MageUI.exe* に渡すことができる PFX ファイルに結合します。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

21. 証明書が生成されたので、顧客は *MageUI.exe* でデプロイマニフェストを開き、保存することによって配置マニフェストに署名するようになりました。 [署名] ダイアログボックスが表示されたら、[ **証明書ファイルとして署名** する] オプションを選択し、ディスクに保存した PFX ファイルを選択します。

22. 顧客は、アプリケーションをユーザーに展開します。

## <a name="see-also"></a>関連項目
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [MakeCert](/windows/desktop/SecCrypto/makecert)
