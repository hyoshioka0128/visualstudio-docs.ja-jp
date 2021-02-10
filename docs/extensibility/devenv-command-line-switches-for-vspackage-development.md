---
title: VSPackage Development の Devenv Command-Line スイッチ |Microsoft Docs
description: 開発者が Visual Studio IDE を起動するファイル devenv.exe を実行するときに、コマンドラインからタスクを自動化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: conceptual
helpviewer_keywords:
- /Setup command line switch
- /ResetSkipPkgs command line switch
- /RootSuffix command line switch
- /SafeMode command line switch
- /Splash command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c6b6260bad412127afe4dd9135ccf66d48e9e3e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968308"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>VSPackage 開発の Devenv コマンド ライン スイッチ

Visual Studio を使用すると、開発者は、Visual Studio IDE を起動するファイルである実行時に、コマンドラインからタスクを自動化でき `devenv.exe` ます。

 タスクには次のものがあります。

- IDE の外部からデザイン済みの構成でアプリケーションを配置する。

- 事前設定されたビルド設定またはデバッグ構成を使用してプロジェクトを自動的にビルドします。

- Ide を特定の構成で読み込みます。すべて IDE の外部からです。 また、起動時に IDE をカスタマイズすることもできます。

## <a name="guidelines-for-switches"></a>スイッチのガイドライン

Visual Studio のドキュメントでは、ユーザーレベルのコマンドラインスイッチについて説明して `devenv` います。 詳細については、「 [Devenv コマンドラインスイッチ](../ide/reference/devenv-command-line-switches.md)」を参照してください。 この `devenv` ツールでは、VSPackage の開発、配置、およびデバッグに役立つその他のコマンドラインスイッチもサポートされています。

| コマンドラインスイッチ | 説明 |
|---------------------| - |
| `/ResetSkipPkgs` | 問題のある Vspackage の読み込みを避ける必要があるユーザーによって追加されたスキップ読み込みオプションをすべてクリアし、Visual Studio を起動します。 SkipLoading タグが存在すると、VSPackage の読み込みが無効になります。 タグをクリアすると、VSPackage の読み込みが再度有効になります。<br /><br /> このスイッチは引数を取りません。 |
| `/RootSuffix` | 別の場所を使用して Visual Studio を起動します。 次のコマンドは、Visual Studio SDK インストーラーによって作成されたショートカットによって実行されます。<br /><br /> `devenv /RootSuffix exp`<br /><br /> この場合、は `exp` 特定のサフィックスを持つ場所 (たとえば、 `10.0Exp` の代わりに) を識別 `10.0` します。 実験用インスタンスを使用すると、コードの記述に使用している Visual Studio のインスタンスとは別に VSPackage をデバッグできます。<br /><br /> このスイッチは、VSRegEx.exe を使用して作成した場所を識別する任意の文字列を受け取ることができます。 詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。 |
| `/SafeMode` | Visual Studio をセーフモードで起動し、既定の IDE とサービスのみを読み込みます。 スイッチは、 `/SafeMode` Visual Studio の起動時にすべてのサードパーティ vspackage が読み込まれないようにし、安定した実行を保証します。<br /><br /> このスイッチは引数を取りません。 |
| `/Setup` | すべての使用可能な Vspackage から、メニュー、ツールバー、およびコマンドグループを記述するリソースメタデータを Visual Studio に強制的にマージします。 このコマンドは、管理者としてのみ実行できます。 <br /><br /> このスイッチは引数を取りません。 `devenv /Setup` コマンドは、一般的にインストール処理の最後の手順として提示されます。 スイッチを使用し `/Setup` ても、IDE は起動しません。|
| `/Splash` | 通常どおり Visual Studio のスプラッシュスクリーンが表示され、メイン IDE が表示される前にメッセージボックスが表示されます。 メッセージボックスを使用すると、スプラッシュスクリーンを調べることができます (たとえば、VSPackage 製品アイコンを確認する場合など)。<br /><br /> このスイッチは引数を取りません。 |

## <a name="see-also"></a>関連項目

- [コマンドラインスイッチの追加](../extensibility/adding-command-line-switches.md)
- [Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)
