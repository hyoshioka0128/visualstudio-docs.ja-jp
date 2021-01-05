---
title: 設定ストアを使用する |Microsoft Docs
description: 読み取り専用の Visual Studio と VSPackage の設定である構成設定ストアからデータを読み取る方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: aeb147c245f7dc09cf91db8a1b810a7c5f30b46b
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715913"
---
# <a name="using-the-settings-store"></a>設定ストアの使用
設定ストアには、次の2種類があります。

- 構成設定。読み取り専用の Visual Studio と VSPackage の設定です。 Visual Studio は、すべての既知の pkgdef ファイルの設定をこのストアにマージします。

- ユーザー設定は、[ **オプション** ] ダイアログボックス、プロパティページ、およびその他の特定のダイアログボックスのページに表示される設定などの書き込み可能な設定です。 Visual Studio 拡張機能では、少量のデータのローカルストレージにこれらを使用できます。

  このチュートリアルでは、構成設定ストアからデータを読み取る方法について説明します。 ユーザー設定ストアに書き込む方法の詳細については [、「ユーザー設定ストアへの書き込み](../extensibility/writing-to-the-user-settings-store.md) 」を参照してください。

## <a name="creating-the-example-project"></a>サンプルプロジェクトの作成
 このセクションでは、デモンストレーション用のメニューコマンドを使用して単純な拡張機能プロジェクトを作成する方法について説明します。

1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]という名前の VSIX プロジェクトを作成 `SettingsStoreExtension` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。

2. 次に、 **Settingsstorecommand** という名前のカスタムコマンド項目テンプレートを追加します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **SettingsStoreCommand.cs** に変更します。 カスタムコマンドを作成する方法の詳細については、「[メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

## <a name="using-the-configuration-settings-store"></a>構成設定ストアの使用
 このセクションでは、構成設定を検出して表示する方法について説明します。

1. SettingsStorageCommand.cs ファイルで、次の using ディレクティブを追加します。

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. で、 `MenuItemCallback` メソッドの本体を削除し、次の行を追加して、構成設定ストアを取得します。

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    は、 <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager> サービスを介したマネージヘルパークラスです <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> 。

3. 次に、Windows Phone ツールがインストールされているかどうかを確認します。 コードは、次のようになります。

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

5. 実験用インスタンスで、[ **ツール** ] メニューの [ **Settingsstorecommand の呼び出し**] をクリックします。

    **Microsoft Windows Phone 開発者ツール** というメッセージボックスが表示されます。その後に **True** または **False** が続きます。

   Visual Studio では、設定ストアはシステムレジストリに保持されます。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>レジストリエディターを使用して構成設定を確認するには

1. Regedit.exe を開きます。

2. HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProductsに移動 \\ します。

    > [!NOTE]
    > \ 14.0Exp_Config \ を含み、14.0_Config ではないキーを見ていることを確認し \\ ます。 Visual Studio の実験用インスタンスを実行すると、構成設定はレジストリハイブ "14.0Exp_Config" にあります。

3. [\ インストールされた製品] ノードを展開します。 前の手順のメッセージが **microsoft Windows Phone 開発者ツールインストールされている場合: True** の場合は、\ インストールされた製品 \ に microsoft Windows Phone 開発者ツールノードが含まれている必要があります。 メッセージが **microsoft Windows Phone 開発者ツールインストールされている場合: False** の場合、[\ インストールされた製品] に microsoft Windows Phone 開発者ツールノードを含めることはできません。
