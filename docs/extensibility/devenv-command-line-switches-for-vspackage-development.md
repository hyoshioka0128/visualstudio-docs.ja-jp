---
title: VSPackage 開発用の Devenv コマンド ライン スイッチ |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad3a5125a730b9230959bbf9342b4c0a4823c4d3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712191"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>VSPackage 開発の Devenv コマンド ライン スイッチ

Visual Studio を使用すると、開発者は、Visual Studio `devenv.exe`IDE を起動するファイルを実行するときに、コマンド ラインからタスクを自動化できます。

 次のようなタスクがあります。

- IDE の外部から、あらかじめ設計された構成でアプリケーションを展開する。

- プリセットビルド設定またはデバッグ構成を使用して、プロジェクトを自動的にビルドします。

- IDE の外部から、特定の構成で IDE をロードします。 起動時に IDE をカスタマイズすることもできます。

## <a name="guidelines-for-switches"></a>スイッチのガイドライン

Visual Studio のドキュメントでは、ユーザー`devenv`レベルのコマンド ライン スイッチについて説明します。 詳細については、「 [Devenv コマンド ライン スイッチ](../ide/reference/devenv-command-line-switches.md)」を参照してください。 この`devenv`ツールは、VSPackage の開発、配置、およびデバッグに役立つ追加のコマンド ライン スイッチもサポートしています。

| コマンドライン スイッチ | 説明 |
|---------------------| - |
| `/ResetSkipPkgs` | 問題のある VSPackage の読み込みを回避するユーザーによって追加されたすべてのスキップ読み込みオプションをクリアし、Visual Studio を起動します。 スキップローディング タグが存在すると、VSPackage の読み込みが無効になります。 タグをクリアすると、VSPackage の読み込みが再度有効になります。<br /><br /> このスイッチは引数を取りません。 |
| `/RootSuffix` | 別の場所を使用して Visual Studio を起動します。 次のコマンドは、Visual Studio SDK インストーラーによって作成されたショートカットによって実行されます。<br /><br /> `devenv /RootSuffix exp`<br /><br /> この場合、`exp`特定のサフィックスを持つ場所を識別`10.0Exp``10.0`します (たとえば、 の代わりに)。 実験用インスタンスを使用すると、コードの記述に使用している Visual Studio のインスタンスとは別に VSPackage をデバッグできます。<br /><br /> このスイッチは、VSRegEx.exe を使用して作成した場所を識別する任意の文字列を受け取ることができます。 詳細については、「[実験インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。 |
| `/SafeMode` | Visual Studio をセーフ モードで起動し、既定の IDE とサービスのみを読み込みます。 スイッチ`/SafeMode`は、Visual Studio の起動時にすべてのサードパーティ製の VSPackage が読み込まれるのを防ぎ、安定した実行を保証します。<br /><br /> このスイッチは引数を取りません。 |
| `/Setup` | Visual Studio で、使用可能なすべての VSPackages のメニュー、ツール バー、およびコマンド グループを記述するリソース メタデータをマージするように強制します。 このコマンドは管理者としてのみ実行できます。 <br /><br /> このスイッチは引数を取りません。 `devenv /Setup` コマンドは、一般的にインストール処理の最後の手順として提示されます。 スイッチを`/Setup`使用しても IDE は起動しません。|
| `/Splash` | いつものように Visual Studio のスプラッシュ画面を表示し、メインの IDE を表示する前にメッセージ ボックスを表示します。 メッセージ ボックスでは、スプラッシュ スクリーンを調査できます (たとえば、VSPackage 製品アイコンを確認する)。<br /><br /> このスイッチは引数を取りません。 |

## <a name="see-also"></a>関連項目

- [コマンド ライン スイッチを追加する](../extensibility/adding-command-line-switches.md)
- [Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)
