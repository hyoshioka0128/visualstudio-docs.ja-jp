---
title: ユーザー設定ストアに書き込んでいます |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 764d9b81297c6bbefd1f5fdf7c77e4d514bb5045
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842045"
---
# <a name="writing-to-the-user-settings-store"></a>ユーザー設定ストアへの書き込み
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザー設定は、[ツール]、[ **オプション** ] ダイアログボックス、[プロパティ] ウィンドウ、およびその他の特定のダイアログボックスのような書き込み可能な設定です。 Visual Studio 拡張機能では、これらを使用して少量のデータを格納できます。 このチュートリアルでは、ユーザー設定ストアからの読み取りと書き込みによって、Visual Studio にメモ帳を外部ツールとして追加する方法について説明します。  
  
### <a name="backing-up-your-user-settings"></a>ユーザー設定のバックアップ  
  
1. デバッグして手順を繰り返すには、外部ツールの設定をリセットできる必要があります。 これを行うには、元の設定を保存して、必要に応じて復元できるようにする必要があります。  
  
2. Regedit.exe を開きます。  
  
3. [HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\14.0Exp\External ツール] に移動 \\ します。  
  
    > [!NOTE]
    > \ 14.0 ではなく、\ 14.0を含むキーを見ていることを確認し \\ ます。 Visual Studio の実験用インスタンスを実行すると、ユーザー設定はレジストリハイブ "14.0 Exp" にあります。  
  
4. [\ 外部ツール \ サブキー] を右クリックし、[ **エクスポート**] をクリックします。 選択した **ブランチ** が選択されていることを確認します。  
  
5. 生成された外部のツール .reg ファイルを保存します。  
  
6. 後で、外部ツールの設定をリセットする場合は、[HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\14.0Exp\External Tools \ レジストリキー] を選択し、コンテキストメニューの [ **削除** ] をクリックします。  
  
7. [ **キーの削除の確認** ] ダイアログボックスが表示されたら、[ **はい**] をクリックします。  
  
8. 前の手順で保存した外部のツール .reg ファイルを右クリックし、[ファイルを **開くアプリケーション**の選択] をクリックして、[ **レジストリエディター**] をクリックします。  
  
## <a name="writing-to-the-user-settings-store"></a>ユーザー設定ストアへの書き込み  
  
1. UserSettingsStoreExtension という名前の VSIX プロジェクトを作成し、Usersettingsstoreextension という名前のカスタムコマンドを追加します。 カスタムコマンドを作成する方法の詳細については、「[メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. UserSettingsStoreCommand.cs で、次の using ステートメントを追加します。  
  
    ```csharp  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    ```  
  
3. MenuItemCallback で、メソッドの本文を削除し、次のようにユーザー設定ストアを取得します。  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);  
    }  
    ```  
  
4. メモ帳が外部ツールとして既に設定されているかどうかを確認します。 次のように、すべての外部ツールを反復処理して、ToolCmd 設定が "Notepad" であるかどうかを確認する必要があります。  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);  
  
        // Find out whether Notepad is already an External Tool.  
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");  
        bool hasNotepad = false;  
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;  
        for (int i = 0; i < toolCount; i++)  
        {  
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)  
            {  
                hasNotepad = true;  
                break;  
            }  
        }  
    }  
  
    ```  
  
5. メモ帳が外部ツールとして設定されていない場合は、次のように設定します。  
  
    ```vb  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);  
  
        // Find out whether Notepad is already installed.  
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");  
        bool hasNotepad = false;  
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;  
        for (int i = 0; i < toolCount; i++)  
        {  
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)  
            {  
                hasNotepad = true;  
                break;  
            }  
        }  
  
        string message = (hasNotepad) ? "Notepad already installed" : "Installing Notepad";  
         if (!hasNotepad)  
        {  
            userSettingsStore.SetString("External Tools", "ToolTitle" + toolCount, "&Notepad");  
            userSettingsStore.SetString("External Tools", "ToolCmd" + toolCount, "C:\\Windows\\notepad.exe");  
            userSettingsStore.SetString("External Tools", "ToolArg" + toolCount, "");  
            userSettingsStore.SetString("External Tools", "ToolDir" + toolCount, "$(ProjectDir)");  
            userSettingsStore.SetString("External Tools", "ToolSourceKey" + toolCount, "");  
            userSettingsStore.SetUInt32("External Tools", "ToolOpt" + toolCount, 0x00000011);  
  
            userSettingsStore.SetInt32("External Tools", "ToolNumKeys", toolCount + 1);  
        }  
    }  
    ```  
  
6. コードをテストします。 メモ帳は外部ツールとして追加されるので、2回目に実行する前にレジストリをロールバックする必要があることに注意してください。  
  
7. コードをビルドし、デバッグを開始します。  
  
8. [ **ツール** ] メニューの [ **UserSettingsStoreCommand の呼び出し**] をクリックします。 これにより、[ **ツール** ] メニューにメモ帳が追加されます。  
  
9. [ツール] メニューの [オプション] メニューにメモ帳が表示され **、メモ帳をクリックする** とメモ帳のインスタンスが表示されます。
