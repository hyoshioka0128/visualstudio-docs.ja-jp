---
title: Vspackage のトラブルシューティング |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a231d8d02ce7432188053293684d09c7243dfd5e
ms.sourcegitcommit: 260d093d2287ba791f28bdc7103493beabf80b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77506402"
---
# <a name="troubleshooting-vspackages"></a>VSPackage のトラブルシューティング
次に、VSPackage と問題を解決するためのヒントについて、一般的な問題を示します。

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>Visual Studio を起動し続ける VSPackage のトラブルシューティングを行うには

- セーフモードで [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を開始します。

   セーフモードで [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を開始するには、コマンドプロンプトで「 **devenv.exe/セーフ**モード」と入力します。

   このプロセスでは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]に含まれている Vspackage を除き、Vspackage は読み込まれません。

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>読み込まれない VSPackage のトラブルシューティングを行うには

1. VSPackage が実行されるように登録されているレジストリルートを使用していることを確認します。通常は実験的なレジストリルートです。

    詳細については、[実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

2. VSPackage が実験的なレジストリルートで実行されるように設定されている場合は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]の実験用バージョンを実行していることを確認してください。

    実験的なバージョンを実行するには、コマンドウィンドウに「 **devenv/rootsuffix exp**」と入力します。

3. VSPackage レジストリエントリを確認します。

    詳細については、「 [vspackage の登録](registering-and-unregistering-vspackages.md)と[vspackage の管理](../extensibility/managing-vspackages.md)」を参照してください。

4. VSPackage の読み込みに失敗した [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のインスタンスの**出力**ウィンドウを開きます。 VSPackage が読み込みに失敗した理由に関する情報が、そのウィンドウに表示されることがあります。

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) から [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の実験用バージョンを起動している場合は、両方のバージョンの**出力**ウィンドウを調べます。

5. アクティビティログを確認します。

    詳細については、「[方法: アクティビティログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

6. IDE によってスローされた例外の詳細については、 **[デバッグ]** メニューの **[例外]** をクリックして、例外を有効にします。 **[例外]** ダイアログボックスで、詳細情報を表示する例外の種類を選択します。

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>登録されていない VSPackage のトラブルシューティングを行うには

1. VSPackage アセンブリが信頼できる場所に配置されていることを確認します。 RegPkg は、既定の .net セキュリティ構成のネットワーク共有など、信頼されていない場所または部分的に信頼できる場所にアセンブリを登録することはできません。 信頼できない場所にユーザーがプロジェクトを作成するたびに警告が表示されますが、[次回からこのメッセージを表示しない] チェックボックスをオンにすると、この警告が再発しないことがあります。

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>コマンドをクリックしたときに表示されない、またはエラーが発生するコマンドのトラブルシューティングを行うには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コマンドプロンプトで次のように入力して、新規または変更されたメニューコマンドと IDE 内の既存のコマンドをマージ**します。**

2. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] が VSPackage の UI を見つけられることを確認します。

   1. レジストリの Packages セクションで、VSPackage の CLSID を探します。

        HKLM\Software\Microsoft\Visual Studio\\ *\<バージョン >* \ パッケージ

   2. SatelliteDll サブキーによって指定されたパスが正しいことを確認します。

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>予期せず動作する VSPackage のトラブルシューティングを行うには

1. コード内にブレークポイントを設定します。

     デバッグの開始点としては、コンストラクターと初期化メソッドを使用することをお勧めします。 また、メニューコマンドなど、評価する領域にブレークポイントを設定することもできます。 ブレークポイントを有効にするには、デバッガーでを実行する必要があります。

    1. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

    2. **[プロパティページ]** ダイアログボックスで、 **[デバッグ]** タブを選択します。

    3. **[コマンドライン引数]** ボックスに、VSPackage が対象とする開発環境のルートサフィックスを入力します。 たとえば、実験用ビルドを選択するには、「 **/rootsuffix Exp**」と入力します。

    4. **[デバッグ]** メニューの **[デバッグの開始]** をクリックするか、F5 キーを押します。

        > [!NOTE]
        > プロジェクトをデバッグする場合は、今すぐプロジェクトの既存のインスタンスを作成するか、読み込んでください。

2. アクティビティログを使用します。

     キーポイントでアクティビティログに情報を書き込むことによって、VSPackage の動作をトレースします。 この手法は、小売環境で VSPackage を実行する場合に特に便利です。 詳細については、「[方法: アクティビティログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

3. パブリックシンボルを使用します。

     デバッグ中の読みやすさを向上させるために、デバッガーにシンボルをアタッチできます。

    1. [ツール] メニューの [オプション] を**選択**し、[デバッグ] **/[シンボル**] ダイアログボックスに移動します。

    2. 次**のシンボルファイル (.pdb) の場所**を追加します。

         `https://msdl.microsoft.com/download/symbols`

    3. パフォーマンスを向上させるには、シンボルキャッシュフォルダーを指定します。次に例を示します。

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>不足している VSPackage またはその依存関係の1つをトラブルシューティングするには

1. マネージコードの場合は、参照パスが正しいことを確認します。

   1. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

   2. **[プロパティページ]** ダイアログボックスの **[参照]** タブを選択し、すべてのパスが正しいことを確認します。 または、**オブジェクトブラウザー**を使用して、参照先のオブジェクトを参照することもできます。

        マネージコードの場合は、 [fuslogvw.exe (アセンブリバインディングログビューアー)](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer)を使用して、失敗したアセンブリの読み込みの詳細を表示できます。

2. アンマネージコードの場合は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] CLSID レジストリノードで VSPackage の CLSID を見つけます。

    HKLM\Software\Microsoft\Visual Studio\\ *\<バージョン >* /CLSID

   InprocServer32 エントリが VSPackage dll の正しいパスを持っていることを確認します。

## <a name="see-also"></a>参照
- [VSPackage](../extensibility/internals/vspackages.md)