---
title: CreatePkgDef Utility |Microsoft Docs
description: Visual Studio 拡張機能の .dll ファイルをパラメーターとして受け取り、.dll ファイルに付随する pkgdef ファイルを作成する CreatePkgDef ユーティリティについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: aa0b0e3e8ea59ce1d41f9d8a6c056239f2bc0e9a
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305542"
---
# <a name="createpkgdef-utility"></a>CreatePkgDef ユーティリティ
は、Visual Studio 拡張機能の .dll ファイルをパラメーターとして受け取り、 *.dll* ファイルに付随する *pkgdef* ファイルを作成します。 *Pkgdef* ファイルには、拡張機能のインストール時にシステムレジストリに書き込まれるすべての情報が含まれています。

> [!NOTE]
> Visual Studio SDK に含まれているほとんどのプロジェクトテンプレートは、ビルド処理の一部として、自動的に *pkgdef* ファイルを作成します。 このドキュメントは、手動でパッケージを作成する場合や、 *pkgdef*  の展開を使用するように既存のパッケージを変換する場合を対象としています。

## <a name="syntax"></a>構文

```
CreatePkgDef /out=<FileName> [/codebase] [/assembly] <AssemblyPath>
```

## <a name="arguments"></a>引数
**/out = &lt; ファイル名&gt;**\
必須。 *Pkgdef* 出力ファイルの名前を FileName に設定し &lt; ます &gt; 。

**/codebase**\
任意。 **CodeBase** ユーティリティに強制的に登録します。

**/assembly**\
**アセンブリ** ユーティリティに登録を強制します。

**&lt;AssemblyPath&gt;**\
*Pkgdef* を生成する元となる *.dll* ファイルのパス。

## <a name="remarks"></a>Remarks
*Pkgdef* ファイルを使用した拡張機能の展開では、以前のバージョンの Visual Studio のレジストリ要件が置き換えられています。

::: moniker range=">=vs-2019"

*Pkgdef* ファイルは、次のいずれかの場所にインストールする必要があります。

- *%localappdata%\Microsoft\Visual Studio\16.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

インストールフォルダーが *%Localappdata%\Microsoft\Visual Studio\16.0\Extensions \\* の場合、拡張機能は Visual Studio によって認識されますが、既定では無効になっています。 ユーザーは、[ **拡張機能の管理**] を使用して拡張機能を有効にすることができます。

インストールフォルダーが *%vsinstalldir%\Common7\IDE\Extensions \\* の場合、拡張機能は既定で有効になっています。

> [!NOTE]
> 拡張 **機能の管理** ツールは、VSIX パッケージの一部としてインストールされている場合を除き、拡張機能にアクセスするためには使用できません。

::: moniker-end

::: moniker range="vs-2017"

*Pkgdef* ファイルは、次のいずれかの場所にインストールする必要があります。

- *%localappdata%\Microsoft\Visual Studio\15.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

インストールフォルダーが *%Localappdata%\Microsoft\Visual Studio\15.0\Extensions \\* の場合、拡張機能は Visual Studio によって認識されますが、既定では無効になっています。 ユーザーは、 **拡張機能と更新プログラム** を使用して拡張機能を有効にすることができます。

インストールフォルダーが *%vsinstalldir%\Common7\IDE\Extensions \\* の場合、拡張機能は既定で有効になっています。

> [!NOTE]
> 拡張機能 **と更新プログラム** ツールは、VSIX パッケージの一部としてインストールされている場合を除き、拡張機能にアクセスするためには使用できません。

::: moniker-end

## <a name="see-also"></a>関連項目
- [Createのインスタンスユーティリティ](../../extensibility/internals/createexpinstance-utility.md)
