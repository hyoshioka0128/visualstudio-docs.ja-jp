---
title: 設定ストアからサービス情報を取得しています |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b15d5c9f122ca66d21940b9998969b0d39d1a74d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80711373"
---
# <a name="get-service-information-from-the-settings-store"></a>設定ストアからサービス情報を取得する
設定ストアを使用して、使用可能なすべてのサービスを検索したり、特定のサービスがインストールされているかどうかを判断したりできます。 サービスクラスの型を把握している必要があります。

## <a name="to-list-the-available-services"></a>利用可能なサービスを一覧表示するには

1. という名前の VSIX プロジェクトを作成し、と `FindServicesExtension` いう名前のカスタムコマンドを追加し `FindServicesCommand` ます。 カスタムコマンドを作成する方法の詳細については、「[メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

2. *FindServicesCommand.cs*で、次の using ディレクティブを追加します。

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. 構成設定ストアを取得し、[サービス] という名前のサブコレクションを検索します。 このコレクションには、利用可能なすべてのサービスが含まれます。 メソッドで、 `MenuItemCommand` 既存のコードを削除し、次のコードに置き換えます。

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

5. 実験用インスタンスで、[ **ツール** ] メニューの [ **Findサービスコマンドの呼び出し**] をクリックします。

     すべてのサービスを一覧表示するメッセージボックスが表示されます。

     これらの設定を確認するには、レジストリエディターを使用します。

## <a name="find-a-specific-service"></a>特定のサービスを検索する
 また、メソッドを使用し <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> て、特定のサービスがインストールされているかどうかを確認することもできます。 サービスクラスの型を把握している必要があります。

1. 前の手順で作成したプロジェクトの MenuItemCallback で、構成設定ストアで、 `Services` サービスの GUID によって指定されたサブコレクションが含まれているコレクションを検索します。 この例では、ヘルプサービスを検索します。

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

3. 実験用インスタンスで、[ **ツール** ] メニューの [ **Findサービスコマンドの呼び出し**] をクリックします。

     " **Help Service Available**  " というテキストが表示されます。その後に **True** または **False**が続きます。 この設定を確認するには、前の手順で示したように、レジストリエディターを使用します。
