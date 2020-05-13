---
title: 設定ストアの使用 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b3bbc09586f883e067e32f525a0331c1a9e253f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698514"
---
# <a name="using-the-settings-store"></a>設定ストアの使用
設定ストアには、次の 2 種類があります。

- 構成設定は、読み取り専用の Visual Studio および VSPackage の設定です。 Visual Studio では、すべての既知の .pkgdef ファイルの設定がこのストアにマージされます。

- ユーザー設定は、**オプション**ダイアログ ボックス、プロパティ ページ、およびその他の特定のダイアログ ボックスのページに表示される設定など、書き込み可能な設定です。 Visual Studio 拡張機能では、少量のデータをローカルに格納するためにこれらを使用できます。

  このチュートリアルでは、構成設定ストアからデータを読み取る方法を示します。 [ユーザー設定ストアへの書き込](../extensibility/writing-to-the-user-settings-store.md)み方法については、「ユーザー設定ストアへの書き込み」を参照してください。

## <a name="creating-the-example-project"></a>サンプル プロジェクトの作成
 このセクションでは、デモンストレーション用のメニュー コマンドを使用して、単純な拡張プロジェクトを作成する方法を示します。

1. すべての Visual Studio 拡張機能は、拡張機能の資産を含む VSIX 配置プロジェクトで開始します。 という名前[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]`SettingsStoreExtension`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、[**新しいプロジェクト**] ダイアログの **[Visual C# / 拡張性**] の下にあります。

2. 次に **、SettingsStoreCommand**という名前のカスタム コマンド項目テンプレートを追加します。 [**新しい項目の追加]** ダイアログで **、[Visual C# / 拡張性**] に移動し、[カスタム**コマンド**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を**SettingsStoreCommand.cs**に変更します。 カスタム コマンドの作成方法の詳細については、「メニュー[コマンドを使用した拡張機能の作成」を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

## <a name="using-the-configuration-settings-store"></a>構成設定ストアの使用
 このセクションでは、構成設定を検出して表示する方法を示します。

1. SettingsStorageCommand.cs ファイルに、次の using ディレクティブを追加します。

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. で`MenuItemCallback`メソッドの本体を削除し、これらの行を追加して構成設定ストアを取得します。

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager>は、サービスに対するマネージ<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager>ヘルパー クラスです。

3. Windows Phone ツールがインストールされているかどうかを確認します。 コードは、次のようになります。

   ```
   private void MenuItemCallback(object sender, EventArgs e)
   {
       SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
       SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
       bool arePhoneToolsInstalled = configurationSettingsStore.CollectionExists(@"InstalledProducts\Microsoft Windows Phone Developer Tools");
       string message = "Microsoft Windows Phone Developer Tools: " + arePhoneToolsInstalled;
       MessageBox.Show(message);
   }
   ```

4. コードをテストします。 プロジェクトをビルドし、デバッグを開始します。

5. 実験用インスタンスの [**ツール**] メニューで、[**設定ストア コマンドの呼び出し**] をクリックします。

    **Windows の電話開発者ツール**を示すメッセージ ボックスが表示されます: **True**または**False**が続きます。

   設定ストアはシステム レジストリに保持されます。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>レジストリ エディターを使用して構成設定を確認するには

1. Regedit.exe を開きます。

2. HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\14.0Exp_Config\インストールされた製品に\\移動します。

    > [!NOTE]
    > \14.0_Config ではなく \14.0Exp_Config\ を含むキーを確認してください\\。 Visual Studio の実験用インスタンスを実行すると、構成設定はレジストリ ハイブ "14.0Exp_Config" に含まれます。

3. [インストール済み製品\ ] ノードを展開します。 前の手順でメッセージが**Microsoft Windows Phone 開発者ツールがインストールされている場合: True**をインストールし、\インストールされている製品\ には、Microsoft Windows の電話開発者ツール のノードが含まれている必要があります。 メッセージが**Microsoft Windows Phone 開発者ツールがインストールされている場合: False**、\インストールされている製品\ には Microsoft Windows Phone 開発者ツール ノードを含めないようにする必要があります。
