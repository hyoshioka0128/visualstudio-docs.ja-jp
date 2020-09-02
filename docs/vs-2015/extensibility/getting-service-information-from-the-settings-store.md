---
title: 設定ストアからサービス情報を取得しています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cfe754203ae9b4e951de5beef8cd829f9d7716bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204315"
---
# <a name="getting-service-information-from-the-settings-store"></a>設定ストアからのサービス情報の取得
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

設定ストアを使用して、使用可能なすべてのサービスを検索したり、特定のサービスがインストールされているかどうかを判断したりできます。 サービスクラスの型を把握している必要があります。  
  
### <a name="to-list-the-available-services"></a>利用可能なサービスを一覧表示するには  
  
1. FindServicesExtension という名前の VSIX プロジェクトを作成し、Findservicecommand という名前のカスタムコマンドを追加します。 カスタムコマンドを作成する方法の詳細については、「[メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. FindServicesCommand.cs で、次の using ステートメントを追加します。  
  
    ```vb  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    using System.Windows.Forms;  
    ```  
  
3. 構成設定ストアを取得し、[サービス] という名前のサブコレクションを検索します。 このコレクションには、利用可能なすべてのサービスが含まれます。 MenuItemCommand メソッドで、既存のコードを削除し、次のコードに置き換えます。  
  
    ```  
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
  
## <a name="finding-a-specific-service"></a>特定のサービスの検索  
 また、メソッドを使用し <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> て、特定のサービスがインストールされているかどうかを確認することもできます。 サービスクラスの型を把握している必要があります。  
  
1. 前の手順で作成したプロジェクトの MenuItemCallback で、構成設定ストアで、 `Services` サービスの GUID によって指定されたサブコレクションが含まれているコレクションを検索します。 この例では、ヘルプサービスを検索します。  
  
    ```  
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
