---
title: プロファイル ツールのコマンド ライン ツールへのパスの指定 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7047bf18-5779-4f6e-872c-66e2fc47c969
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f66ed17aec8c6e5303ea61741021dd25032fcb37
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75406303"
---
# <a name="specify-the-path-to-profiling-tools-command-line-tools"></a>プロファイル ツールのコマンド ライン ツールへのパスの指定

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのコマンド ライン ツールのパスは、PATH 環境変数に追加されません。 32 ビット コンピューターでは、これらのツールは単一のディレクトリ内にあります。 64 ビット コンピューターには、32 ビット バージョンと 64 ビット バージョンの両方のプロファイリング ツールがあります。

## <a name="32-bit-computers"></a>32 ビット コンピューター

ネイティブ コード用の Visual Studio プロファイラー API は *VSPerf.dll* にあります。 ヘッダー ファイル *VSPerf.h* とインポート ライブラリ *VSPerf.lib* は、*Microsoft Visual Studio\2017\Team Tools\Performance Tools\PerfSDK* ディレクトリにあります。

 マネージド コード用のプロファイラー API は、*Microsoft.VisualStudio.Profiler.dll* にあります。 この DLL は、*Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools* ディレクトリにあります。

## <a name="64-bit-computers"></a>64 ビット コンピューター

64 ビット コンピューターでは、プロファイリングするアプリケーションのターゲット プラットフォームに応じてパスを指定します。

- 32 ビット アプリケーションの場合、既定のプロファイリング ツール ディレクトリは以下のとおりです。

     (ネイティブ) *Microsoft Visual Studio\2017\Team Tools\Performance Tools\PerfSDK*
     
     (マネージド) *Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools*

- 64 ビット アプリケーションの場合、既定のプロファイリング ツール ディレクトリは以下のとおりです。

     (ネイティブ) *Microsoft Visual Studio\2017\Team Tools\Performance Tools\x64\PerfSDK*

     (マネージド) *Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools\x64*
