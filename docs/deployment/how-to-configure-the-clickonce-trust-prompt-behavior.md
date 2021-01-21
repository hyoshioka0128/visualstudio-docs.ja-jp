---
title: ClickOnce 信頼プロンプトの動作を構成する |Microsoft Docs
description: Clickonce 信頼プロンプトを構成して、ClickOnce アプリケーションをインストールするオプションをエンドユーザーに付与するかどうかを制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- deploying applications [ClickOnce], trust prompt
- ClickOnce applications, install without prompting
- ClickOnce applications, trust prompt
- ClickOnce deployment, trust prompt
ms.assetid: cc04fa75-012b-47c9-9347-f4216be23cf2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68d39bed64ff1392c83d6fc2be0de936ac1b00d2
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94350063"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>方法: ClickOnce 信頼プロンプトの動作を構成する
ClickOnce 信頼プロンプトを構成して、Windows フォームアプリケーション、Windows Presentation Foundation アプリケーション、コンソールアプリケーション、WPF ブラウザーアプリケーション、Office ソリューションなど、ClickOnce アプリケーションをインストールするオプションをエンドユーザーに付与するかどうかを制御できます。 信頼プロンプトを構成するには、各エンドユーザーのコンピューターでレジストリキーを設定します。

 次の表は、5つのゾーン (Internet、UntrustedSites、MyComputer、LocalIntranet、および TrustedSites) のそれぞれに適用できる構成オプションを示しています。

|オプション|レジストリ設定値|説明|
|------------|----------------------------|-----------------|
|信頼プロンプトを有効にします。|`Enabled`|ClickOnce 信頼プロンプトが表示されるので、エンドユーザーは ClickOnce アプリケーションに信頼を与えることができます。|
|信頼プロンプトを制限します。|`AuthenticodeRequired`|ClickOnce 信頼プロンプトは、ClickOnce アプリケーションが発行者を識別する証明書で署名されている場合にのみ表示されます。|
|信頼プロンプトを無効にします。|`Disabled`|明示的に信頼された証明書で署名されていない ClickOnce アプリケーションに対しては、ClickOnce 信頼プロンプトは表示されません。|

 次の表は、各ゾーンの既定の動作を示しています。 [アプリケーション] 列は、Windows フォームアプリケーション、Windows Presentation Foundation アプリケーション、WPF ブラウザーアプリケーション、コンソールアプリケーションを指します。

|ゾーン|アプリケーション|Office ソリューション|
|----------|------------------|----------------------|
|`MyComputer`|`Enabled`|`Enabled`|
|`LocalIntranet`|`Enabled`|`Enabled`|
|`TrustedSites`|`Enabled`|`Enabled`|
|`Internet`|`Enabled`|`AuthenticodeRequired`|
|`UntrustedSites`|`Disabled`|`Disabled`|

 ClickOnce 信頼プロンプトを有効にしたり、制限したり、無効にしたりすることで、これらの設定をオーバーライドできます。

## <a name="enable-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを有効にする
 ゾーンから取得した ClickOnce アプリケーションをインストールして実行するオプションをエンドユーザーに表示させる場合は、ゾーンの信頼プロンプトを有効にします。

#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリエディターを使用して ClickOnce 信頼プロンプトを有効にするには

1. レジストリエディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. [ **名前** ] ボックスに「 `regedit` 」と入力し、[ **OK** ] をクリックします。

2. 次のレジストリキーを探します。

     **\ HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\ 。NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、 **文字列値** として追加します。次の表に、関連する値を示します。

    |文字列値サブキー|[値]|
    |-------------------------|-----------|
    |`Internet`|`Enabled`|
    |`UntrustedSites`|`Disabled`|
    |`MyComputer`|`Enabled`|
    |`LocalIntranet`|`Enabled`|
    |`TrustedSites`|`Enabled`|

     Office ソリューションの場合、には既定値があり、には値が設定されてい `Internet` `AuthenticodeRequired` `UntrustedSites` `Disabled` ます。 それ以外の場合、に `Internet` は既定値が設定さ `Enabled` れます。

#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムで有効にするには

1. Visual Studio で Visual Basic または Visual C# コンソールアプリケーションを作成します。

2. 編集するために、 *プログラム .vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "Enabled")
    key.SetValue("TrustedSites", "Enabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Enabled");
    key.SetValue("LocalIntranet", "Enabled");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "Enabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. アプリケーションをビルドして実行します。

## <a name="restrict-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを制限する
 信頼のプロンプトを制限して、ユーザーが信頼の決定を求められる前に、既知の id を持つ Authenticode 証明書を使用してソリューションに署名する必要があるようにします。

#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリエディターを使用して ClickOnce 信頼プロンプトを制限するには

1. レジストリエディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. [ **名前** ] ボックスに「 `regedit` 」と入力し、[ **OK** ] をクリックします。

2. 次のレジストリキーを探します。

     **\ HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\ 。NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、 **文字列値** として追加します。次の表に、関連する値を示します。

    |文字列値サブキー|[値]|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`AuthenticodeRequired`|
    |`MyComputer`|`AuthenticodeRequired`|
    |`LocalIntranet`|`AuthenticodeRequired`|
    |`TrustedSites`|`AuthenticodeRequired`|

#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムで制限するには

1. Visual Studio で Visual Basic または Visual C# コンソールアプリケーションを作成します。

2. 編集するために、 *プログラム .vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "AuthenticodeRequired")
    key.SetValue("LocalIntranet", "AuthenticodeRequired")
    key.SetValue("Internet", "AuthenticodeRequired")
    key.SetValue("TrustedSites", "AuthenticodeRequired")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "AuthenticodeRequired");
    key.SetValue("LocalIntranet", "AuthenticodeRequired");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "AuthenticodeRequired");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. アプリケーションをビルドして実行します。

## <a name="disable-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを無効にする
 信頼プロンプトを無効にして、エンドユーザーに対して、セキュリティポリシーでまだ信頼されていないソリューションをインストールするオプションがないようにすることができます。

#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリエディターを使用して ClickOnce 信頼プロンプトを無効にするには

1. レジストリエディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. [ **名前** ] ボックスに「 `regedit` 」と入力し、[ **OK** ] をクリックします。

2. 次のレジストリキーを探します。

     **\ HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\ 。NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、 **文字列値** として追加します。次の表に、関連する値を示します。

    |文字列値サブキー|[値]|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`Disabled`|
    |`MyComputer`|`Disabled`|
    |`LocalIntranet`|`Disabled`|
    |`TrustedSites`|`Disabled`|

#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムで無効にするには

1. Visual Studio で Visual Basic または Visual C# コンソールアプリケーションを作成します。

2. 編集するために、 *プログラム .vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Disabled")
    key.SetValue("LocalIntranet", "Disabled")
    key.SetValue("Internet", "Disabled")
    key.SetValue("TrustedSites", "Disabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Disabled");
    key.SetValue("LocalIntranet", "Disabled");
    key.SetValue("Internet", "Disabled");
    key.SetValue("TrustedSites", "Disabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();

    ```

3. アプリケーションをビルドして実行します。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [信頼されたアプリケーションの展開の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法: ClickOnce アプリケーションのセキュリティゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタムアクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [方法: ClickOnce アプリケーション用の信頼された発行者をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: アプリケーション マニフェストおよび配置マニフェストに再署名する](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
