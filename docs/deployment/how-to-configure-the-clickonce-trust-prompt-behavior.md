---
title: '方法 : ClickOnce 信頼プロンプトの動作を構成する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: ec5f1cca49f1b799b39969849e0a73bf1e6e296d
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649147"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>方法: ClickOnce 信頼プロンプトの動作を構成する
Windows フォーム アプリケーション、Windows プレゼンテーション 基盤アプリケーション、コンソール アプリケーション、WPF ブラウザー アプリケーション、Office ソリューションなどの ClickOnce アプリケーションをインストールするかどうかをエンド ユーザーに許可するかどうかを制御する、ClickOnce 信頼プロンプトを構成できます。 各エンド ユーザーのコンピュータにレジストリ キーを設定して、信頼プロンプトを構成します。

 次の表は、5 つのゾーン (インターネット、信頼されていないサイト、マイ コンピュータ、ローカル イントラネット、および信頼済みサイト) それぞれに適用できる構成オプションを示しています。

|オプション|レジストリ設定値|説明|
|------------|----------------------------|-----------------|
|信頼プロンプトを有効にします。|`Enabled`|エンド ユーザーが ClickOnce アプリケーションに信頼を付与できるように、ClickOnce 信頼プロンプトが表示されます。|
|信頼プロンプトを制限します。|`AuthenticodeRequired`|ClickOnce 信頼プロンプトは、ClickOnce アプリケーションが発行元を識別する証明書で署名されている場合にのみ表示されます。|
|信頼プロンプトを無効にします。|`Disabled`|明示的に信頼された証明書を使用して署名されていない ClickOnce アプリケーションに対して、ClickOnce 信頼プロンプトは表示されません。|

 次の表は、各ゾーンの既定の動作を示しています。 [アプリケーション] 列は、Windows フォーム アプリケーション、Windows プレゼンテーション ファンデーション アプリケーション、WPF ブラウザー アプリケーション、およびコンソール アプリケーションを示します。

|ゾーン|アプリケーション|Office ソリューション|
|----------|------------------|----------------------|
|`MyComputer`|`Enabled`|`Enabled`|
|`LocalIntranet`|`Enabled`|`Enabled`|
|`TrustedSites`|`Enabled`|`Enabled`|
|`Internet`|`Enabled`|`AuthenticodeRequired`|
|`UntrustedSites`|`Disabled`|`Disabled`|

 これらの設定をオーバーライドするには、ClickOnce 信頼プロンプトを有効にするか、制限するか、無効にします。

## <a name="enable-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを有効にする
 エンド ユーザーに対して、そのゾーンから取得した ClickOnce アプリケーションをインストールして実行するオプションを表示する場合は、ゾーンの信頼プロンプトを有効にします。

#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリ エディターを使用して ClickOnce 信頼プロンプトを有効にするには

1. レジストリ エディタを開きます。

    1. **[スタート]** ボタンをクリックして **[ファイル名を指定して実行]** をクリックします。

    2. [**ファイル**] ボックスに`regedit`「OK」と入力し **、[OK]** をクリックします。

2. 次のレジストリ キーを検索します。

     **\HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\\.NET フレームワーク\セキュリティ\トラストマネージャー\プロンプトレベル**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、次の表に示す関連する値を文字列**値**として追加します。

    |文字列値サブキー|値|
    |-------------------------|-----------|
    |`Internet`|`Enabled`|
    |`UntrustedSites`|`Disabled`|
    |`MyComputer`|`Enabled`|
    |`LocalIntranet`|`Enabled`|
    |`TrustedSites`|`Enabled`|

     Office ソリューションの`Internet`場合、既定値を`AuthenticodeRequired`持`UntrustedSites`ち、値`Disabled`が設定されます。 その他の場合`Internet`は、デフォルト値`Enabled`を持ちます。

#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムで有効にするには

1. Visual Studio で Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集用の*Program.vb*ファイルまたは*Program.cs*ファイルを開き、次のコードを追加します。

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
 信頼の決定をユーザーに求める前に、既知の ID を持つ Authenticode 証明書を使用してソリューションに署名する必要がある場合は、信頼プロンプトを制限します。

#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリ エディターを使用して ClickOnce 信頼プロンプトを制限するには

1. レジストリ エディタを開きます。

    1. **[スタート]** ボタンをクリックして **[ファイル名を指定して実行]** をクリックします。

    2. [**ファイル**] ボックスに`regedit`「OK」と入力し **、[OK]** をクリックします。

2. 次のレジストリ キーを検索します。

     **\HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\\.NET フレームワーク\セキュリティ\トラストマネージャー\プロンプトレベル**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、次の表に示す関連する値を文字列**値**として追加します。

    |文字列値サブキー|値|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`AuthenticodeRequired`|
    |`MyComputer`|`AuthenticodeRequired`|
    |`LocalIntranet`|`AuthenticodeRequired`|
    |`TrustedSites`|`AuthenticodeRequired`|

#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムで制限するには

1. Visual Studio で Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集用の*Program.vb*ファイルまたは*Program.cs*ファイルを開き、次のコードを追加します。

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
 信頼プロンプトを無効にして、エンド ユーザーがセキュリティ ポリシーで信頼されていないソリューションをインストールするオプションを与えないようにすることができます。

#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリ エディターを使用して ClickOnce 信頼プロンプトを無効にするには

1. レジストリ エディタを開きます。

    1. **[スタート]** ボタンをクリックして **[ファイル名を指定して実行]** をクリックします。

    2. [**ファイル**] ボックスに`regedit`「OK」と入力し **、[OK]** をクリックします。

2. 次のレジストリ キーを検索します。

     **\HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\\.NET フレームワーク\セキュリティ\トラストマネージャー\プロンプトレベル**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、次の表に示す関連する値を文字列**値**として追加します。

    |文字列値サブキー|値|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`Disabled`|
    |`MyComputer`|`Disabled`|
    |`LocalIntranet`|`Disabled`|
    |`TrustedSites`|`Disabled`|

#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムで無効にするには

1. Visual Studio で Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集用の*Program.vb*ファイルまたは*Program.cs*ファイルを開き、次のコードを追加します。

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
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法 : ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [方法: ClickOnce アプリケーション用の信頼された発行者をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: アプリケーション マニフェストおよび配置マニフェストに再署名する](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
