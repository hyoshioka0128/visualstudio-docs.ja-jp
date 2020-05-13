---
title: Visual Studio でのテンプレート検出のトラブルシューティング |マイクロソフトドキュメント
ms.date: 01/02/2018
ms.topic: conceptual
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 078d06c797c3b228c1ea5b1d836dceb0394b3174
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698933"
---
# <a name="troubleshooting-template-installation"></a>テンプレートのインストールのトラブルシューティング

プロジェクトまたは項目テンプレートの配置に関する問題が発生した場合は、診断ログを有効にできます。

::: moniker range="vs-2017"

1. インストールする*共通\IDE\CommonExtensions*フォルダーに pkgdef ファイルを作成します。 たとえば *、C:\プログラム ファイル (x86)\マイクロソフト ビジュアル スタジオ\2017\エンタープライズ\コモン7\IDE\コモンエクステンション\EnablePkgDefLogging.pkgdef*。

::: moniker-end

::: moniker range=">=vs-2019"

1. インストールする*共通\IDE\CommonExtensions*フォルダーに pkgdef ファイルを作成します。 たとえば *、C:\プログラム ファイル (x86)\マイクロソフト ビジュアル スタジオ\2019\エンタープライズ\コモン7\IDE\コモンエクステンション\EnablePkgDefLogging.pkgdef*。

::: moniker-end

2. pkgdef ファイルに次の項目を追加します。

    ```
    [$RootKey$\VsTemplate]
    "EnableTemplateDiscoveryLog"=dword:00000001
    ```

3. インストール用の[開発者コマンド プロンプト](/dotnet/framework/tools/developer-command-prompt-for-vs)を開き`devenv /updateConfiguration`、 を実行します。

::: moniker range="vs-2017"

4. Visual Studio を開き、両方のテンプレート ツリーを初期化する [新しいプロジェクト] ダイアログ ボックスと [新しい項目] ダイアログ ボックスを起動します。

   テンプレート ログが **%LOCALAPPDATA%%\マイクロソフト\VisualStudio\15.0_[インスタンス ID]\VsTemplateDiagnosticsList.csv**に表示されるようになりました (インスタンス ID は Visual Studio のインスタンスのインストール ID に対応しています)。 各テンプレート ツリーの初期化では、このログにエントリが追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

4. Visual Studio を開き、**新しいプロジェクトの作成**と**新しい項目**のダイアログ ボックスを起動して、両方のテンプレート ツリーを初期化します。

   テンプレート ログが **%LOCALAPPDATA%%\マイクロソフト\VisualStudio\16.0_[インスタンス ID]\VsTemplateDiagnosticsList.csv**に表示されるようになりました (インスタンス ID は Visual Studio のインスタンスのインストール ID に対応しています)。 各テンプレート ツリーの初期化では、このログにエントリが追加されます。

::: moniker-end

ログ ファイルには、次の列が含まれています。

- 次の**値を持**つテンプレートを使用します。

  - マニフェストベースの配置の場合は 1

  - 0 (ディスクベースの展開用)

- **テンプレートファイル名**

- その他のテンプレート プロパティ

> [!NOTE]
> ログを無効にするには、pkgdef ファイルを削除するか、 の`EnableTemplateDiscoveryLog`値を`dword:00000000`に変更してから`devenv /updateConfiguration`もう一度実行します。

## <a name="see-also"></a>関連項目

- [カスタム プロジェクトテンプレートと項目テンプレートの作成](creating-custom-project-and-item-templates.md)
