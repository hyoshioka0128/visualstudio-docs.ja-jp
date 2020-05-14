---
title: ユーザー設定ストアへの書き込み |マイクロソフトドキュメント
ms.date: 05/23/2019
ms.topic: conceptual
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2bed721cc084042c3ebe57639af28b7e9f13d206
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740361"
---
# <a name="writing-to-the-user-settings-store"></a>ユーザー設定ストアへの書き込み
ユーザー設定は、[**ツール] メニューの [オプション]** ダイアログ ボックス、プロパティ ウィンドウ、およびその他のダイアログ ボックスのような書き込み可能な設定です。 Visual Studio 拡張機能では、少量のデータを格納するためにこれらを使用する場合があります。 このチュートリアルでは、ユーザー設定ストアから読み書きすることにより、メモ帳を外部ツールとして Visual Studio に追加する方法を示します。

## <a name="writing-to-the-user-settings-store"></a>ユーザー設定ストアへの書き込み

1. という名前の VSIX プロジェクトを作成し、ユーザー設定ストア コマンドという名前のカスタム コマンドを追加します。 カスタム コマンドの作成方法の詳細については、「メニュー[コマンドを使用した拡張機能の作成」を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

2. UserSettingsStoreCommand.csで、次の using ディレクティブを追加します。

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    ```

3. MenuItemCallback で、メソッドの本体を削除し、次のようにユーザー設定ストアを取得します。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);
    }
    ```

4. メモ帳が既に外部ツールとして設定されているかどうかを確認します。 次のように、すべての外部ツールを反復処理して、ToolCmd 設定が "メモ帳" であるかどうかを判断する必要があります。

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

6. コードをテストします。 メモ帳は外部ツールとして追加されるので、レジストリをもう一度実行する前に、レジストリをロールバックする必要があります。

7. コードをビルドし、デバッグを開始します。

8. [**ツール**] メニューの [**ユーザー設定ストア コマンドの呼び出し**] をクリックします。 これにより、[**ツール]** メニューにメモ帳が追加されます。

9. [ツール] メニューの [オプション] にメモ帳が表示され、[**メモ帳**] をクリックするとメモ帳のインスタンスが表示されます。
