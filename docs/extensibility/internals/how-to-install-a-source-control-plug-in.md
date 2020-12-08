---
title: '方法: ソース管理プラグインをインストールする |Microsoft Docs'
description: Visual studio でソース管理プラグインを Visual studio ソース管理プラグイン API と統合し、その DLL を登録することによって、ソース管理プラグインをインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2496de5d1139d66e4ae9072b551ada990cf856dd
ms.sourcegitcommit: 2f964946d7044cc7d49b3fc10b413ca06cb2d11b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761232"
---
# <a name="how-to-install-a-source-control-plug-in"></a>方法: ソース管理プラグインをインストールする
ソース管理プラグインの作成には、次の3つのステップが含まれます。

1. このドキュメントの「ソース管理プラグイン API リファレンス」で定義されている関数を使用して、DLL を作成します。

2. ソース管理プラグイン API 定義関数を実装します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]が呼び出されたときに、プラグインからインターフェイスとダイアログボックスを使用できるようにします。

3. 適切なレジストリエントリを作成して、DLL を登録します。

## <a name="integration-with-visual-studio"></a>Visual Studio との統合
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、ソース管理プラグイン API に準拠するソース管理プラグインがサポートされています。

### <a name="register-the-source-control-plug-in"></a>ソース管理プラグインを登録する
 実行中の統合開発環境 (IDE) がソース管理システムを呼び出すことができるようにするには、まず、API をエクスポートするソース管理プラグイン DLL を見つける必要があります。

#### <a name="to-register-the-source-control-plug-in-dll"></a>ソース管理プラグイン DLL を登録するには

1. Company name サブキーの後に product name サブキーを指定して、 **SOFTWARE** サブキーの **HKEY_LOCAL_MACHINE** キーの下に2つのエントリを追加します。 パターンは **\\ \<company name> \\HKEY_LOCAL_MACHINE\SOFTWARE\<product name> \\ 値 \<entry>**  =  *value* です。 2つのエントリは、常に **Sccservername** および **Sccserverpath** と呼ばれます。 各は通常の文字列です。

    たとえば、会社名が Microsoft で、ソース管理製品に SourceSafe という名前が付いている場合、このレジストリパスは **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe** になります。 このサブキーでは、最初のエントリ **Sccservername** は、ユーザーが判読できる、製品の名前付きの文字列です。 2番目のエントリである **Sccserverpath** は、IDE が接続するソース管理プラグイン DLL への完全パスです。 レジストリエントリの例を次に示します。

   |レジストリエントリのサンプル|値の例|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerPath|*c:\vss\win32\ssscc.dll*|

   > [!NOTE]
   > SCCServerPath は、SourceSafe プラグインへの完全なパスです。 ソース管理プラグインでは、異なる会社名と製品名が使用されますが、レジストリエントリのパスは同じです。

2. 次のオプションのレジストリエントリを使用して、ソース管理プラグインの動作を変更できます。 これらのエントリは、 **Sccservername** および **Sccserverpath** と同じサブキーで実行されます。

   - **HideInVisualStudioregistry** エントリは、ソース管理プラグインがの **プラグイン選択** リストに表示されないようにする場合に使用でき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 このエントリは、ソース管理プラグインへの自動切り替えにも影響します。 このエントリの使用方法の1つとして、ソース管理プラグインを置き換えるソース管理パッケージを指定する場合がありますが、ソース管理プラグインを使用するからソース管理パッケージへの移行を簡単に行うことをお勧めします。 ソース管理パッケージがインストールされると、このレジストリエントリが設定され、プラグインが非表示になります。

      **HideInVisualStudio** は DWORD 値で、プラグインを非表示にするには *1* に、プラグインを表示するには *0* に設定されています。 レジストリエントリが表示されない場合、既定の動作ではプラグインが表示されます。

   - **Disablesccmanager** レジストリエントリを使用して、通常は [**ファイル** ソース管理] サブメニューに表示される [**起動 \<Source Control Server>** ] メニューオプションを無効または非表示にすることができ  >  **Source Control** ます。 このメニューオプションを選択すると、 [SccRunScc](../../extensibility/sccrunscc-function.md) 関数が呼び出されます。 ソース管理プラグインが外部プログラムをサポートしていない可能性があるため、[ **起動** ] メニューオプションを無効にしたり、非表示にしたりすることもできます。

      **Disablesccmanager** は DWORD 値です。 *0* に設定すると、[**起動 \<Source Control Server>** ] メニューオプションが有効になります。また、メニューオプションを無効にするには *1* に設定し、メニューオプションを非表示にするには [ *2* ] に設定します。 このレジストリエントリが表示されない場合、既定の動作ではメニューオプションが表示されます。

   | レジストリエントリのサンプル | 値の例 |
   | - |--------------|
   | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio | 1 |
   | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\DisableSccManager | 1 |

3. **ソフトウェア** サブキーの **HKEY_LOCAL_MACHINE** キーの下に、サブキー **SourceCodeControlProvider** を追加します。

    このサブキーの下で、レジストリエントリ **Providerregkey** は、手順 1. でレジストリに配置したサブキーを表す文字列に設定されます。 ****  =  *ソフトウェア \\<会社名 \> \\<製品名 \>* HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKeyパターンです。

    このサブキーのサンプルコンテンツを次に示します。

   |レジストリ エントリ|値の例|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > ソース管理プラグインでは同じサブキーとエントリ名が使用されますが、値は異なります。

4. **SourceCodeControlProvider** サブキーの下に、「」という名前のサブキーを作成し、そのサブキー **の下に** 1 つのエントリを配置します。

    このエントリの名前は、ユーザーが判読できるプロバイダーの名前 (SCCServerName エントリに指定された値と同じ) で、値は、手順 1. で作成したサブキーと同じになります。 パターンは、 **\\ 表示 \> 名**  =  *ソフトウェア \\<会社名 \> \\<製品名 \>*<HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProvidersます。

    例:

   |レジストリエントリのサンプル|値の例|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > この方法では、複数のソース管理プラグインを登録できます。 これは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] インストールされているすべてのソース管理プラグイン API ベースのプラグインを検索する方法です。

## <a name="how-an-ide-locates-the-dll"></a>IDE が DLL を検索する方法
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE には、ソース管理プラグイン DLL を検索する方法が2つあります。

- 既定のソース管理プラグインを検索し、サイレントモードで接続します。

- ユーザーが選択した、登録されているすべてのソース管理プラグインを検索します。

  最初の方法で DLL を検索するために、IDE では、入力 **Providerregkey** の **HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider** サブキーが検索されます。 このエントリの値は、別のサブキーを指しています。 次に、 **HKEY_LOCAL_MACHINE** の下の2番目のサブキーで **Sccserverpath** という名前のエントリが検索されます。 このエントリの値により、IDE が DLL を参照します。

> [!NOTE]
> IDE は、相対パス ( *.\NewProvider.DLL* など) から dll を読み込みません。 DLL への完全なパスを指定する必要があります (たとえば、 *c:\Providers\NewProvider.DLL*)。 これにより、未承認または偽装されたプラグイン Dll の読み込みを防ぐことができ、IDE のセキュリティが強化されます。

 2番目の方法で DLL を検索するために、IDE はすべてのエントリに対して **HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider\InstalledSCCProviders** サブキーを検索します。 各エントリには、名前と値があります。 IDE では、これらの名前の一覧がユーザーに表示されます。 ユーザーが名前を選択すると、選択した名前の値が IDE によって検索され、サブキーが参照されます。 IDE は、 **HKEY_LOCAL_MACHINE** の下で、そのサブキーに **Sccserverpath** という名前のエントリを検索します。 このエントリの値は、IDE で正しい DLL を指しています。

 ソース管理プラグインは、DLL を検索する両方の方法をサポートする必要があります。その結果、 **Providerregkey** が設定され、以前の設定が上書きされます。 さらに重要なこととして、ユーザーが使用するソース管理プラグインを選択できるように、それ自体をインストールされている **Sccproviders** の一覧に追加する必要があります。

> [!NOTE]
> **HKEY_LOCAL_MACHINE** キーが使用されるため、特定のコンピューターに既定のソース管理プラグインとして登録できるソース管理プラグインは1つだけです (ただし、ユーザーは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 特定のソリューションに対して実際に使用するソース管理プラグインを決定できます)。 インストールプロセス中に、ソース管理プラグインが既に設定されているかどうかを確認します。その場合は、インストールする新しいソース管理プラグインを既定として設定するかどうかをユーザーに確認してください。 アンインストール中に、 **HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider** のすべてのソース管理プラグインに共通する他のレジストリサブキーを削除しないでください。特定の SCC サブキーのみを削除します。

## <a name="how-the-ide-detects-version-1213-support"></a>IDE がバージョン 1.2/1.3 サポートを検出する方法
 で [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プラグインがソース管理プラグイン API バージョン1.2 と1.3 の機能をサポートしているかどうかを検出する方法 高度な機能を宣言するには、ソース管理プラグインが対応する関数を実装する必要があります。

 まず、は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [Sccgetversion](../../extensibility/sccgetversion-function.md)を呼び出して返された値をチェックします。 1.2 以上である必要があります。

 次に、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] `lpSccCaps` [sccinitialize](../../extensibility/sccinitialize-function.md)の引数を調べて、特定の新機能がサポートされているかどうかを判断します。

 これら両方の条件が満たされている場合は、バージョン1.2 および1.3 でサポートされている新しい関数を呼び出すことができます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインを使ってみる](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
