---
title: 設定ストアからのサービス情報の取得 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b15d5c9f122ca66d21940b9998969b0d39d1a74d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711373"
---
# <a name="get-service-information-from-the-settings-store"></a>設定ストアからサービス情報を取得する
設定ストアを使用して、利用可能なすべてのサービスを検索したり、特定のサービスがインストールされているかどうかを確認したりできます。 サービス クラスの型を知っている必要があります。

## <a name="to-list-the-available-services"></a>利用可能なサービスを一覧表示するには

1. という名前`FindServicesExtension`の VSIX プロジェクトを作成し、という`FindServicesCommand`名前のカスタム コマンドを追加します。 カスタム コマンドの作成方法の詳細については、「メニュー[コマンドを使用して拡張機能を作成する」を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

2. *FindServicesCommand.cs*で、次の using ディレクティブを追加します。

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. 構成設定ストアを取得し、Services という名前のサブコレクションを見つけます。 このコレクションには、使用可能なすべてのサービスが含まれます。 メソッドで`MenuItemCommand`既存のコードを削除し、次のコードに置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string message = "Available services:\n";
        IEnumerable<string> collection = configurationSettingsStore.GetSubCollectionNames("Services");
        int n = 0;
        foreach (string service in collection)
        {
            message += configurationSettingsStore.GetString("Services\\" + service, "Name", "Unknown") + "\n";
        }

        MessageBox.Show(message);
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. 実験用インスタンスの [**ツール**] メニューの **[FindServicesCommand の呼び出し**] をクリックします。

     すべてのサービスを一覧表示するメッセージ ボックスが表示されます。

     これらの設定を確認するには、レジストリ エディタを使用します。

## <a name="find-a-specific-service"></a>特定のサービスを検索する
 このメソッドを使用して<xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A>、特定のサービスがインストールされているかどうかを確認することもできます。 サービス クラスの型を知っている必要があります。

1. 前の手順で作成したプロジェクトの MenuItemCallback で、構成設定ストアで、サービスの`Services`GUID によって名前が付けられたサブコレクションを持つコレクションを検索します。 この場合、ヘルプ サービスを探します。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string helpServiceGUID = typeof(SVsHelpService).GUID.ToString("B").ToUpper();
        bool hasHelpService = configurationSettingsStore.CollectionExists("Services\\" + helpServiceGUID);
        string message = "Help Service Available: " + hasHelpService;

        MessageBox.Show(message);
    }
    ```

2. プロジェクトをビルドし、デバッグを開始します。

3. 実験用インスタンスの [**ツール**] メニューの **[FindServicesCommand の呼び出し**] をクリックします。

     **ヘルプ サービスが利用可能**なというテキストのメッセージが表示され、その後に**True**または False が表示**されます**。 この設定を確認するには、前の手順で示したように、レジストリ エディタを使用します。
