---
title: '方法 : ソース管理プラグインをインストールする |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c0ac87aec3d6ac2532909772238e020e33bf78f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707993"
---
# <a name="how-to-install-a-source-control-plug-in"></a>方法: ソース管理プラグインをインストールする
ソース管理プラグインの作成には、次の 3 つの手順が含まれます。

1. このドキュメントの「ソース管理プラグイン API リファレンス」セクションで定義されている関数を使用して DLL を作成します。

2. ソース管理プラグイン API 定義関数を実装します。 呼[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]び出し時に、プラグインからインターフェイスとダイアログ ボックスを使用できるようにします。

3. 適切なレジストリ エントリを作成して、DLL を登録します。

## <a name="integration-with-visual-studio"></a>Visual Studio との統合
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、ソース管理プラグイン API に準拠するソース管理プラグインをサポートします。

### <a name="register-the-source-control-plug-in"></a>ソース管理プラグインを登録します。
 実行中の統合開発環境 (IDE) がソース管理システムを呼び出す前に、API をエクスポートするソース管理プラグイン DLL を最初に見つける必要があります。

#### <a name="to-register-the-source-control-plug-in-dll"></a>ソース管理プラグイン DLL を登録するには

1. 会社名サブキーの後に製品名サブキーを指定する **、SOFTWARE**サブキーの**HKEY_LOCAL_MACHINE**キーの下に 2 つのエントリを追加します。 このパターンは **、製品名\\\<>製品名\\\<>値>HKEY_LOCAL_MACHINE\SOFTWARE\\\<社名です***。*  =  2 つのエントリは常に**SCC サーバー名**と**SCC サーバー パス**と呼ばれます。 各文字列は通常の文字列です。

    たとえば、会社名が Microsoft で、ソース管理製品の名前が SourceSafe の場合、このレジストリ パスは**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe**になります。 このサブキーでは、最初のエントリ**SCCServerName**は、製品の名前を付けるユーザーが読み取り可能な文字列です。 2 番目のエントリ**SCCServerPath**は、IDE が接続するソース管理プラグイン DLL への完全パスです。 次に、サンプル のレジストリ エントリを示します。

   |サンプル レジストリ エントリ|値の例|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\ソースセーフ\SCCサーバー名|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\ソースセーフ\SCCサーバーパス|*c:\vss\win32\ssscc.dll*|

   > [!NOTE]
   > SCCServerPath は、ソース セーフ プラグインへの完全パスです。 ソース管理プラグインは、異なる会社名と製品名を使用しますが、同じレジストリ エントリ パスを使用します。

2. 次のオプションのレジストリ エントリを使用して、ソース管理プラグインの動作を変更できます。 これらのエントリは **、SccServerName**および**SccServerPath**と同じサブキーに入ります。

   - **HideInVisualStudio レジストリ**エントリは、ソース管理プラグインをプラグインの選択リストに表示しない場合に使用できます。 **Plug-in Selection** [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] このエントリは、ソース管理プラグインへの自動切り替えにも影響します。 このエントリの使用目的の 1 つとして、ソース管理プラグインを置き換えるソース管理パッケージを提供するが、ソース管理プラグインを使用してソース管理パッケージに移行しやすくする場合があります。 ソース管理パッケージをインストールすると、このレジストリ エントリが設定され、プラグインが非表示になります。

      **HideInVisualStudio**は DWORD 値であり、プラグインを非表示にするには*1*に設定され、プラグインを表示するには*0*に設定されています。 レジストリ エントリが表示されない場合、既定の動作ではプラグインが表示されます。

   - **DisableSccManager**レジストリ エントリを使用すると、通常は **[ファイル** > ソース管理]**サブメニュー**の下に表示される [**ソース管理サーバーの起動\<>]** メニュー オプションを無効または非表示にすることができます。 このメニュー オプションを選択すると[、SccRunScc](../../extensibility/sccrunscc-function.md)関数が呼び出されます。 ソース管理プラグインは外部プログラムをサポートしていない可能性があるため、[**起動**] メニュー オプションを無効にしたり非表示にすることもできます。

      **DisableSccManager**は DWORD 値であり *、0*に設定され、**ソース管理サーバーの起動\<メニュー**オプション>メニュー オプションを有効にし *、1*に設定してメニュー オプションを無効にし *、2*に設定してメニュー オプションを非表示にします。 このレジストリ エントリが表示されない場合は、メニュー オプションが表示されます。

   | サンプル レジストリ エントリ | 値の例 |
   | - |--------------|
   | HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\ソースセーフ\隠しビジュアルスタジオ | 1 |
   | HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\ソースセーフ\無効にする | 1 |

3. **ソフトウェア**サブキーの**HKEY_LOCAL_MACHINE**キーの下に、サブキー**を**追加します。

    このサブキーの下で、レジストリ エントリ**ProviderRegKey**は、手順 1 でレジストリに配置したサブキーを表す文字列に設定されます。 パターンは**HKEY_LOCAL_MACHINE\SOFTWARE\ソースコードコントロールプロバイダ\プロバイダレジストリキー** = *ソフトウェア\\<会社名<\>\\製品名\>* です。

    このサブキーのサンプル コンテンツを次に示します。

   |レジストリ エントリ|値の例|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE\ソフトウェア\ソースコードコントロールプロバイダ\プロバイダレジストリキー|ソフトウェア\マイクロソフト\ソースセーフ|

   > [!NOTE]
   > ソース管理プラグインは、同じサブキーとエントリ名を使用しますが、値は異なります。

4. という**名前の**サブキーを作成します。 **SourceCodeControlProvider**

    このエントリの名前はプロバイダのユーザーが読める名前 (SCCServerName エントリに指定された値と同じ) であり、値は手順 1 で作成されたサブキーです。 パターンは**\\HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders<表示名\>***\\\>\\\>* = ソフトウェア<会社名<製品名です。

    次に例を示します。

   |サンプル レジストリ エントリ|値の例|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\ソフトウェア\ソースコードコントロールプロバイダ\インストールされたSCCプロバイダ\マイクロソフトビジュアルソースセーフ|ソフトウェア\マイクロソフト\ソースセーフ|

   > [!NOTE]
   > この方法で登録された複数のソース管理プラグインを使用できます。 この方法[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]で、インストールされているすべてのソース管理プラグイン API ベースのプラグインを検索します。

## <a name="how-an-ide-locates-the-dll"></a>IDE が DLL を検索する方法
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE には、ソース管理プラグイン DLL を検索する 2 つの方法があります。

- 既定のソース管理プラグインを見つけて、サイレント モードで接続します。

- ユーザーがプラグインを選択する、登録されているすべてのソース管理プラグインを検索します。

  最初の方法で DLL を見つけるには、IDE はエントリ**ProviderRegKey**の**HKEY_LOCAL_MACHINE\ソフトウェア\ソースコードコントロールプロバイダ**サブキーの下を検索します。 このエントリの値は、別のサブキーを指します。 次に、IDE は HKEY_LOCAL_MACHINE の下の 2 番目のサブキーで**SccServerPath**という名前のエントリ**を**探します。 このエントリの値は、IDE が DLL を指します。

> [!NOTE]
> 相対パス (*たとえば、.\NewProvider.DLL)* から DLL は読み込まれません。 DLL への完全パスを指定する必要があります (*たとえば、c:\プロバイダー\NewProvider.DLL)。* これにより、許可されていないプラグイン DLL や偽装されたプラグイン DLL の読み込みを防止することで、IDE のセキュリティが強化されます。

 2 番目の方法で DLL を見つけるには、IDE は**HKEY_LOCAL_MACHINE\ソフトウェア\ソースコードコントロールプロバイダ\InstalledSCCProviders**サブキーの下にすべてのエントリを検索します。 各エントリには、名前と値があります。 IDE では、これらの名前のリストがユーザーに表示されます。 ユーザーが名前を選択すると、選択した名前の値がサブキーを指す値が検索されます。 IDE は、 の下のサブキーで**SccServerPath**という名前のエントリ**HKEY_LOCAL_MACHINE**探します。 エントリの値は、IDE に正しい DLL を指定します。

 ソース管理プラグインは、DLL を検索する両方の方法をサポートする必要があり、その結果 **、ProviderRegKey**を設定して、以前の設定を上書きします。 さらに重要なのは、ユーザーが使用するソース管理プラグインを選択できるように **、InstalledSccProviders**の一覧に自分自身を追加する必要があります。

> [!NOTE]
> **HKEY_LOCAL_MACHINE**キーが使用されるため、特定のマシン上のデフォルトのソース管理プラグインとして登録できるのは 1 つのソース管理プラグインのみです (ただし、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ユーザーは、実際に特定のソリューションに使用するソース管理プラグインを決定できます)。 インストールプロセス中に、ソース管理プラグインが既に設定されているかどうかを確認します。インストールされている場合は、インストールする新しいソース管理プラグインをデフォルトとして設定するかどうかをユーザーに確認します。 アンインストール中に **、HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider**のすべてのソース管理プラグインに共通する他のレジストリ サブキーを削除しないでください。特定の SCC サブキーのみを削除します。

## <a name="how-the-ide-detects-version-1213-support"></a>IDE がバージョン 1.2/1.3 のサポートを検出する方法
 プラグインが[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理プラグイン API バージョン 1.2 および 1.3 の機能をサポートしているかどうかをどのように検出しますか? 高度な機能を宣言するには、ソース管理プラグインは、対応する関数を実装する必要があります。

 まず[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)][、SccGetVersion](../../extensibility/sccgetversion-function.md)を呼び出して返される値をチェックします。 1.2 以上である必要があります。

 次に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、 [SccInitialize](../../extensibility/sccinitialize-function.md)の引数を調べること`lpSccCaps`によって、特定の新しい機能がサポートされているかどうかを確認します。

 これらの条件の両方が満たされている場合、バージョン 1.2 および 1.3 でサポートされる新しい関数を呼び出すことができます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの使用を開始する](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
