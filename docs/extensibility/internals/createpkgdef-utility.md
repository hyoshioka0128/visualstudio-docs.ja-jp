---
title: PkgDef ユーティリティを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package definition
- create pkgdef
- pkgdef
- createpkgdef
ms.assetid: c745cb76-47a6-49ff-9eed-16af0f748e35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9f437eb3586dc16bb0b4b9eb60cd303eb90db6c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709165"
---
# <a name="createpkgdef-utility"></a>ユーティリティを作成します。
Visual Studio 拡張機能の .dll ファイルをパラメーターとして受け取り *、.dll*ファイルに付属する *.pkgdef*ファイルを作成します。 *pkgdef*ファイルには、拡張機能のインストール時にシステム レジストリに書き込まれるすべての情報が含まれています。

> [!NOTE]
> Visual Studio SDK に含まれているほとんどのプロジェクト テンプレートは、ビルド プロセスの一部として *.pkgdef*ファイルを自動的に作成します。 このドキュメントは、パッケージを手動で作成する場合や、既存のパッケージを *.pkgdef*展開を使用するように変換する場合を想定しています。

## <a name="syntax"></a>構文

```
CreatePkgDef /out=<FileName> [/codebase] [/assembly] <AssemblyPath>
```

## <a name="arguments"></a>引数
**/out=&lt;ファイル名&gt;**\
必須。 *pkgdef*出力ファイルの名前をファイル名&lt;&gt;に設定します。

**/コードベース**\
省略可能。 **CodeBase**ユーティリティを使用して強制的に登録します。

**/アセンブリ**\
アセンブリ ユーティリティを使用して強制的に登録**します**。

**&lt;アセンブリパス&gt;**\
*pkgdef*を生成する *.dll*ファイルのパス。

## <a name="remarks"></a>Remarks
*pkgdef*ファイルを使用した拡張機能の配置は、以前のバージョンの Visual Studio のレジストリ要件に置き換えられます。

::: moniker range=">=vs-2019"

*pkgdef*ファイルは、次のいずれかの場所にインストールする必要があります。

- *%ローカルアプリケーションデータ%\マイクロソフト\ビジュアルスタジオ\16.0\拡張機能\\*

- *%vsinstalldir%\共通7\IDE\拡張機能\\*

インストール フォルダーが *%localappdata%\Microsoft\Visual Studio\16.0\\\拡張機能*である場合、拡張機能は Visual Studio によって認識されますが、既定では無効になっています。 ユーザーは、拡張機能の管理 を使用して**拡張機能を**有効にすることができます。

インストール フォルダが *%vsinstalldir%\Common7\IDE\Extensions\\*の場合、拡張機能は既定で有効になっています。

> [!NOTE]
> **拡張機能の管理**ツールは、VSIX パッケージの一部としてインストールされていない拡張にアクセスするために使用できません。

::: moniker-end

::: moniker range="vs-2017"

*pkgdef*ファイルは、次のいずれかの場所にインストールする必要があります。

- *%ローカルアプリケーションデータ%\マイクロソフト\ビジュアルスタジオ\15.0\拡張機能\\*

- *%vsinstalldir%\共通7\IDE\拡張機能\\*

インストール フォルダーが *%localappdata%\Microsoft\Visual Studio\15.0\\\拡張機能*である場合、拡張機能は Visual Studio によって認識されますが、既定では無効になっています。 ユーザーは、拡張機能と更新プログラムを使用して**拡張機能を**有効にすることができます。

インストール フォルダが *%vsinstalldir%\Common7\IDE\Extensions\\*の場合、拡張機能は既定で有効になっています。

> [!NOTE]
> **拡張機能と更新**ツールは、VSIX パッケージの一部としてインストールされていない限り、拡張機能にアクセスするために使用できません。

::: moniker-end

## <a name="see-also"></a>関連項目
- [ユーティリティを作成します。](../../extensibility/internals/createexpinstance-utility.md)
