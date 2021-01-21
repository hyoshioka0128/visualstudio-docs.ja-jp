---
title: '方法: 信頼のリストのセキュリティを構成する'
description: 信頼の決定を包含リストに保存することによって、Office ソリューションをインストールするオプションをエンドユーザーに付与するかどうかを制御するには、ClickOnce の信頼プロンプトを構成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1f9eca5150e019906805adf40e5c9b6af8a3c14e
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846728"
---
# <a name="how-to-configure-inclusion-list-security"></a>方法: 信頼のリストのセキュリティを構成する
  管理者のアクセス許可を持っている場合は、信頼の決定を [信頼の [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 決定] の一覧に保存することによって、エンドユーザーに Office ソリューションのインストールオプションを提供するかどうかを制御する信頼プロンプトを構成できます。 包含リストの詳細については、「 [信頼リストを使用した Office ソリューションの信頼](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)」を参照してください。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 5つのゾーンそれぞれに含まれるソリューションでは、次のオプションを設定できます。

- [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信頼プロンプトキーと信頼の一覧を有効にします。 エンドユーザーが、任意の証明書で署名された Office ソリューションに信頼を付与できるようにすることができます。

- [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信頼プロンプトキーと信頼の一覧を制限します。 発行者を識別する証明書で署名された Office ソリューションをエンドユーザーがインストールできるようにすることができますが、これはまだ信頼されていません。

- [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信頼プロンプトキーと信頼の一覧を無効にします。 明示的に信頼された証明書で署名されていない Office ソリューションをエンドユーザーがインストールできないようにすることができます。

## <a name="enable-the-inclusion-list"></a>信頼のリストを有効にする
 ゾーンから取得した Office ソリューションをインストールして実行するオプションをエンドユーザーに表示させる場合は、ゾーンの信頼の一覧を有効にします。

### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>レジストリエディターを使用して、信頼の一覧を有効にするには

1. レジストリエディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. [ **名前** ] ボックスに「 **regedt32.exe**」と入力し、[ **OK**] をクリックします。

2. 次のレジストリキーを探します。

     **\ HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\ 。NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、それに関連付けられた値を使用して、 **文字列値** として追加します。

    |文字列値サブキー|[値]|
    |-------------------------|-----------|
    |**Internet**|**AuthenticodeRequired**|
    |**UntrustedSites**|**Disabled**|
    |**MyComputer**|**有効**|
    |**LocalIntranet**|**有効**|
    |**TrustedSites**|**有効**|

     既定では、 **インターネット** の値は **AuthenticodeRequired** 、 **Untrustedsites** の値は **無効になっ** ています。

### <a name="to-enable-the-inclusion-list-programmatically"></a>プログラムによって信頼の一覧を有効にするには

1. Visual Basic または Visual C# コンソールアプリケーションを作成します。

2. 編集するために、 *プログラム .vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "AuthenticodeRequired")
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

## <a name="restrict-the-inclusion-list"></a>包含リストを制限する
 信頼の決定を求めるメッセージが表示される前に、既知の id を持つ Authenticode 証明書を使用してソリューションに署名する必要があるように、信頼の一覧を制限します。

### <a name="to-restrict-the-inclusion-list"></a>包含一覧を制限するには

1. レジストリエディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. [ **名前** ] ボックスに「 **regedt32.exe**」と入力し、[ **OK**] をクリックします。

2. 次のレジストリキーを探します。

     **\ HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\ 。NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、作成します。

3. 次のサブキーが存在しない場合は、それに関連付けられた値を使用して、 **文字列値** として追加します。

    |文字列値サブキー|[値]|
    |-------------------------|-----------|
    |**UntrustedSites**|**Disabled**|
    |**Internet**|**AuthenticodeRequired**|
    |**MyComputer**|**AuthenticodeRequired**|
    |**LocalIntranet**|**AuthenticodeRequired**|
    |**TrustedSites**|**AuthenticodeRequired**|

     既定では、 **インターネット** の値は **AuthenticodeRequired** 、 **Untrustedsites** の値は **無効になっ** ています。

### <a name="to-restrict-the-inclusion-list-programmatically"></a>プログラムによって包含一覧を制限するには

1. Visual Basic または Visual C# コンソールアプリケーションを作成します。

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

## <a name="disable-the-inclusion-list"></a>信頼の一覧を無効にする
 信頼できる証明書で署名されているソリューションのみをエンドユーザーがインストールできるように、信頼の一覧を無効にすることができます。

### <a name="to-disable-the-inclusion-list"></a>信頼の一覧を無効にするには

1. レジストリエディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. [ **名前** ] ボックスに「 **regedt32.exe**」と入力し、[ **OK**] をクリックします。

2. まだ存在しない場合は、次のレジストリキーを作成します。

     **\ HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\ 。NETFramework\Security\TrustManager\PromptingLevel**

3. 次のサブキーが存在しない場合は、それに関連付けられた値を使用して、 **文字列値** として追加します。

    |文字列値サブキー|[値]|
    |-------------------------|-----------|
    |**UntrustedSites**|**Disabled**|
    |**Internet**|**Disabled**|
    |**MyComputer**|**Disabled**|
    |**LocalIntranet**|**Disabled**|
    |**TrustedSites**|**Disabled**|

### <a name="to-disable-the-inclusion-list-programmatically"></a>プログラムによって信頼の一覧を無効にするには

1. Visual Basic または Visual C# コンソールアプリケーションを作成します。

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
- [信頼リストを使用して Office ソリューションを信頼する](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
