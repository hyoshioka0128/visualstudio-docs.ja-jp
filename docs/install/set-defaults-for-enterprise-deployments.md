---
title: エンタープライズ展開に既定値を設定する
description: Visual Studio のエンタープライズ展開で使用するドメイン ポリシーとその他の構成操作について説明します。
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- gpo
- policy
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 9B7B4608-7A3F-4FF4-BDCE-42D9F7CE6DBA
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 305b0398550a64722f6029a3d50082e6397643cb
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594527"
---
# <a name="set-defaults-for-enterprise-deployments-of-visual-studio"></a>Visual Studio のエンタープライズ展開に既定値を設定する

Visual Studio の展開に影響するレジストリ ポリシーを設定することができます。 これらのポリシーは新しいインストーラーに対してグローバルであり、次に対する影響があります。

- 他のバージョンまたはインスタンスと共有されているパッケージがいくつかインストールされている場合
- パッケージがキャッシュされている場合
- すべてのパッケージがキャッシュされている場合

これらのポリシーのいくつかを[コマンド ライン オプション](use-command-line-parameters-to-install-visual-studio.md)を使用して設定してコンピューターのレジストリ値を設定できるだけでなく、グループ ポリシーを使用して組織全体にこれらを配布することもできます。

## <a name="registry-keys"></a>レジストリ キー

一部の場所ではエンタープライズの既定を設定して、グループ ポリシーを使用するかレジストリから直接、管理を有効にすることができます。 Visual Studio は順番にエンタープライズ ポリシーが設定されているかを確認し、以下の順番でポリシー値が検出された時点で、残りのキーは無視されます。

1. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\Setup`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup`
3. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\VisualStudio\Setup` (64 ビット オペレーティング システム)

> [!IMPORTANT]
> `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\Setup` キーを設定せず、代わりの他のキーのいずれかを設定する場合は、他の両方のキーを 64 ビット オペレーティング システムに設定する必要があります。 この問題は、製品の将来の更新プログラムで対処されます。

いくつかのレジストリ値は、未設定の場合、最初に使われたときに自動的に設定されます。 これにより、以後のインストールでも同じ値が使われるようになります。 これらの値は、2 番目のレジストリ キーである `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup` に格納されます。

以下のレジストリ値を設定できます。

| **Name** | **Type** | **default** | **説明** |
| -------- | -------- | ----------- | --------------- |
| `CachePath` | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages | パッケージ マニフェストと、ペイロード (省略可能) が格納されるディレクトリ。 詳しくは、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページをご覧ください。 |
| `KeepDownloadedPayloads` | `REG_DWORD` | 1 | パッケージのペイロードはインストール後も保持されます。 この値はいつでも変更できます。 ポリシーを無効にすると、修復または変更するインスタンスでキャッシュされたパッケージのペイロードがすべて削除されます。 詳しくは、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページをご覧ください。 |
| `SharedInstallationPath` | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared | Visual Studio の異なるバージョンのインスタンスで共有されているパッケージがいくつかインストールされているディレクトリ。 値はいつでも変更できますが、変更が反映されるのは以後のインストールのみです。 元の場所に既にインストールされている製品は移動しないでください。移動すると、正しく機能しない場合があります。 |
| `BackgroundDownloadDisabled` |`REG_DWORD` | 1 | インストールされているすべての Visual Studio 製品に対して、更新プログラムが自動的にダウンロードされないようにします。 この値はいつでも変更できます。 |

> [!IMPORTANT]
> インストール後に `CachePath` のレジストリ ポリシーを変更する場合は、既存のパッケージ キャッシュを新しい場所に移動して、`SYSTEM` および `Administrators` にフル コントロールが、`Everyone` に読み取りアクセスが可能になるようにセキュリティを保護する必要があります。
> 既存のキャッシュの移動やセキュリティの保護に失敗すると、今後のインストールで問題が発生する場合があります。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

- [Visual Studio のインストール](install-visual-studio.md)
- [パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)
- [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
