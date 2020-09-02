---
title: Visual Studio の検索 |Microsoft Docs
ms.date: 08/21/2017
ms.topic: conceptual
helpviewer_keywords:
- deployment, VSIX
ms.assetid: 680c3b25-7901-4768-8363-6d1fcd1ea636
ms.author: heaths
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a7187fbcc3e3aca990846176676a47f5d17aaf00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "64878144"
---
# <a name="locate-visual-studio"></a>Visual Studio を探す

Visual Studio 2017 以降では、同じバージョンまたはエディションの複数のインスタンスをインストールできます。 これは、以前のインストールを維持しながら、プライマリ開発用コンピューターで新しい機能をプレビューする場合に便利です。 これらの変更のため、インスタンスの検索に使用できる1つの環境変数またはレジストリ値はありません。 代わりに、 [COM クエリ API](https://msdn.microsoft.com/library/microsoft.visualstudio.setup.configuration.aspx) を使用して、拡張機能に関連する条件に基づいてインスタンスを検索することができます。

これは、ネイティブコードとマネージコードで使用できる NuGet パッケージを含む高速で読み取り専用の API です。

| コード | Package |
| ---- | --- |
| ネイティブ | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Native |
| マネージド | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Interop |

パスまたは現在のプロセスを指定して単一のインスタンスを検索することも、すべてのインスタンスを列挙することもできます。 Visual Studio を検索する方法の完全な例については [、サンプル](https://github.com/Microsoft/vs-setup-samples) を参照してください。

## <a name="tools"></a>ツール

ビルド環境、PowerShell スクリプト、インストーラー、その他のシナリオで Visual Studio やその他のツールを見つけるには、独自のスクリプトと共に直接または再配布できるオープンソースツールが多数あります。

| プロジェクト | 説明 |
| ------- | ----------- |
| [vswhere](https://github.com/Microsoft/vswhere) | 1つのファイルのネイティブ実行可能ファイルで、リリースやプレリリース、インストールされている製品、インストールされているワークロードなどの条件を満たすインスタンスを検索します。 では、visual studio 2010 以降を検索することもできます。ただし、Visual Studio 2017 以降では、より少ない情報が返されます。 例については、 [wiki](https://github.com/Microsoft/vswhere/wiki) を参照してください。 |
| [VSSetup コマンドレット](https://github.com/Microsoft/vssetup.powershell) | PowerShell コマンドレットは、2.0 以降でサポートされています。これにより、 _vswhere_ と同じ条件に基づいてインスタンスを検索し、インスタンスに関するさらに多くのプロパティを検出するために使用できるオブジェクトとして、豊富な情報が返されます。 例については、 [wiki](https://github.com/Microsoft/vssetup.powershell/wiki) を参照してください。 |
| [VSIXBootstrapper](https://github.com/Microsoft/vsixbootstrapper) | は、 _VSIXInstaller_ を自動的に検索し、コマンドラインを渡して **.vsix* ファイルをインストールします。 この機能は、クエリ Api を直接サポートしていないインストーラーで役に立ちます。 例については、 [wiki](https://github.com/Microsoft/vsixbootstrapper/wiki) を参照してください。 |

## <a name="see-also"></a>関連項目

* [Visual Studio 2017 セットアップの変更点](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup/)
* [DTE を使って Visual Studio を起動する](launch-visual-studio-dte.md)