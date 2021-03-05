---
title: Visual Studio でのテンプレート検出のトラブルシューティング |Microsoft Docs
description: Visual Studio SDK でのカスタムプロジェクトとテンプレートのデプロイに関するトラブルシューティングのために診断ログを有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/02/2018
ms.topic: troubleshooting
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1ea99c1d74c06ab42ff86f07de4cf5c76e95de43
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151325"
---
# <a name="troubleshooting-template-installation"></a>テンプレートインストールのトラブルシューティング

プロジェクトまたは項目テンプレートの配置で問題が発生した場合は、診断ログを有効にすることができます。

::: moniker range="vs-2017"

1. インストール用の *Common7\IDE\CommonExtensions* フォルダーに .pkgdef ファイルを作成します。 たとえば、 *C:\Program files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef* のようになります。

::: moniker-end

::: moniker range=">=vs-2019"

1. インストール用の *Common7\IDE\CommonExtensions* フォルダーに .pkgdef ファイルを作成します。 たとえば、 *C:\Program files (x86) \Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef* のようになります。

::: moniker-end

2. 次のものを .pkgdef ファイルに追加します。

    ```
    [$RootKey$\VsTemplate]
    "EnableTemplateDiscoveryLog"=dword:00000001
    ```

3. インストールの [開発者コマンドプロンプト](../ide/reference/command-prompt-powershell.md) を開き、を実行 `devenv /updateConfiguration` します。

::: moniker range="vs-2017"

4. Visual Studio を開き、[新しいプロジェクト] ダイアログボックスと [新しい項目] ダイアログボックスを起動して、両方のテンプレートツリーを初期化します。

   テンプレートログが **%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_ [instanceid] \VsTemplateDiagnosticsList.csv** に表示されるようになりました (Instanceid は Visual Studio のインスタンスのインストール ID に対応します)。 各テンプレートツリーの初期化で、エントリがこのログに追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

4. Visual Studio を開き、[ **新しいプロジェクトの作成** ] および [ **新しい項目** ] ダイアログボックスを起動して、両方のテンプレートツリーを初期化します。

   テンプレートログが **%LOCALAPPDATA%\Microsoft\VisualStudio\16.0_ [instanceid] \VsTemplateDiagnosticsList.csv** に表示されるようになりました (Instanceid は Visual Studio のインスタンスのインストール ID に対応します)。 各テンプレートツリーの初期化で、エントリがこのログに追加されます。

::: moniker-end

ログファイルには、次の列が含まれています。

- **FullPathToTemplate**: 次の値が含まれます。

  - 1 (マニフェストベースの展開の場合)

  - ディスクベースの展開の場合は0

- **TemplateFileName**

- その他のテンプレートのプロパティ

> [!NOTE]
> ログ記録を無効にするには、.pkgdef ファイルを削除するか、の値 `EnableTemplateDiscoveryLog` をに変更し `dword:00000000` てから、を再度実行し `devenv /updateConfiguration` ます。

## <a name="see-also"></a>関連項目

- [カスタムプロジェクトテンプレートと項目テンプレートの作成](creating-custom-project-and-item-templates.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
