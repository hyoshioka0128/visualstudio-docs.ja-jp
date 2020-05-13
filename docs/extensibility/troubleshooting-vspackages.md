---
title: VS パッケージのトラブルシューティング |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a4827a36bd8e76462a137ae7e903c1ab624121c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698917"
---
# <a name="troubleshooting-vspackages"></a>VSPackage のトラブルシューティング
VSPackage に関する一般的な問題と、問題を解決するためのヒントを次に示します。

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>Visual Studio の起動を妨げないようにする VSPackage のトラブルシューティングを行うには

- セーフ[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]モードで起動します。

   セーフ[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]モードで起動するには、コマンド プロンプトで**devenv.exe /safemode**と入力します。

   このプロセスの間、VSPackages は に含まれている VSPackages[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]以外は読み込まれません。

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>読み込まれない VSPackage のトラブルシューティングを行うには

1. VSPackage が実行されるように登録されているレジストリ ルート (通常は実験用のレジストリ ルート) を使用していることを確認します。

    詳細については、「[実験インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

2. VSPackage が実験用レジストリ ルートで実行される場合は、実験用バージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を実行していることを確認します。

    実験用バージョンを実行するには、コマンド ウィンドウ**に次のように**入力します。

3. VSPackage レジストリ エントリを確認してください。

    詳細については、「 [VS パッケージの登録](registering-and-unregistering-vspackages.md)および VS パッケージ[の管理](../extensibility/managing-vspackages.md)」を参照してください。

4. VSPackage の読み込みに[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]失敗しているインスタンスの **[出力**] ウィンドウを開きます。 VSPackage が読み込みに失敗した理由に関する情報は、そのウィンドウに表示される場合があります。

   > [!NOTE]
   > 統合開発環境 (IDE)[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]からの実験[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版を起動する場合は、両方のバージョンの **「出力**」ウィンドウを調べます。

5. アクティビティ ログを調べます。

    詳細については、「方法[: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

6. IDE によってスローされる例外の詳細については、[**デバッグ**] メニューの [**例外**] をクリックして、例外を有効にします。 [**例外]** ダイアログ ボックスで、詳細情報を取得する例外の種類を選択します。

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>登録されない VSPackage のトラブルシューティングを行うには

1. VSPackage アセンブリが信頼できる場所に存在することを確認します。 RegPkg は、既定の .net セキュリティ構成のネットワーク共有など、信頼されていない場所または部分的に信頼できる場所にアセンブリを登録できません。 ユーザーが信頼できない場所にプロジェクトを作成すると警告が表示されますが、[このメッセージを再度表示しない] チェック ボックスを使用すると、この警告が再発しないようにできます。

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>表示されないコマンド、またはコマンドをクリックしたときにエラーが発生するコマンドのトラブルシューティングを行うには

1. 新しいメニュー コマンドまたは変更されたメニュー コマンドと、既に IDE に[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]存在するコマンドをマージするには、コマンド プロンプト**で次のように**入力します。

2. VSPackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]の UI.dll が見つからないことを確認します。

   1. VSPackage の CLSID をレジストリのパッケージ セクションで見つけます。

        HKLM\ソフトウェア\マイクロソフト\ビジュアルスタジオ\\*\<のバージョン>* \パッケージ

   2. SatelliteDll サブキーによって指定されたパスが正しいことを確認します。

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>予期しない動作をする VSPackage のトラブルシューティングを行うには

1. コード内にブレークポイントを設定します。

     デバッグの開始点として、コンストラクターと初期化メソッドが役立ちます。 また、メニュー コマンドなど、評価する領域にブレークポイントを設定することもできます。 ブレークポイントを有効にするには、デバッガーで実行する必要があります。

    1. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

    2. [**プロパティ ページ**] ダイアログ ボックスで、[**デバッグ**] タブを選択します。

    3. [**コマンド ライン引数**] ボックスに、VSPackage が対象とする開発環境のルート サフィックスを入力します。 たとえば、実験用ビルドを選択するには、**次**のように入力します。

    4. [**デバッグ**] メニューの [**デバッグの開始**] をクリックするか、F5 キーを押します。

        > [!NOTE]
        > プロジェクトをデバッグする場合は、プロジェクトの既存のインスタンスを今すぐ作成またはロードします。

2. アクティビティ ログを使用します。

     キー ポイントでアクティビティ ログに情報を書き込み、VSPackage の動作をトレースします。 この手法は、リテール環境で VSPackage を実行する場合に特に便利です。 詳細については、「方法[: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

3. パブリック シンボルを使用します。

     デバッグ中の読みやすさを向上させるために、デバッガーにシンボルをアタッチできます。

    1. [**ツール] メニューの [オプション]** から[**デバッグ]/[シンボル**] ダイアログ ボックスに移動します。

    2. この**シンボル ファイル (.pdb) の場所を**追加します。

         `https://msdl.microsoft.com/download/symbols`

    3. パフォーマンスを向上させるには、次のようにシンボル キャッシュ フォルダを指定します。

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>VSPackage またはその依存関係の 1 つが見つからない問題をトラブルシューティングするには

1. マネージ コードの場合は、参照パスが正しいことを確認します。

   1. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

   2. [**プロパティ ページ**] ダイアログ ボックスの [**参照**設定] タブを選択し、すべてのパスが正しいことを確認します。 または、**オブジェクト ブラウザ**を使用して参照先のオブジェクトを参照することもできます。

        マネージ コードの場合は[、Fuslogvw.exe (アセンブリ バインディング ログ ビューアー) を](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer)使用して、失敗したアセンブリ読み込みの詳細を表示できます。

2. アンマネージ コードの場合は、CLSID レジストリ ノードで[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSPackage の CLSID を探します。

    HKLM\ソフトウェア\マイクロソフト\ビジュアルスタジオ\\*\<バージョン>* \CLSID

   インプロセスサーバー32 エントリに VSPackage dll の正しいパスがあることを確認します。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
