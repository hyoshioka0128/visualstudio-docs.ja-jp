---
title: サポートされている Roslyn パッケージのバージョンマッピング
description: この記事では、さまざまなバージョンの Visual Studio でサポートされている .NET compiler platform (Roslyn) パッケージのバージョンについて説明します。
ms.custom: SEO-VS-2020
ms.date: 04/29/2019
ms.topic: reference
helpviewer_keywords:
- roslyn package versions
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f76a8dcdbb644fe456c62fca7de6fb7afe96d556
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99935894"
---
# <a name="net-compiler-platform-package-version-reference"></a>.NET compiler platform パッケージバージョンリファレンス

次の表は、さまざまなバージョンの Visual Studio でサポートされている [.net compiler platform (Roslyn) パッケージ](https://www.nuget.org/packages/Microsoft.Net.Compilers/) のバージョンを示しています。

たとえば、カスタムアナライザーが Visual Studio 2017 のすべてのバージョンで動作するようにするには、バージョン2.0 の Microsoft.Net をターゲットにする必要があります。

| Roslyn パッケージのバージョン | サポートされる Visual Studio の最小バージョン |
| - | - |
| 3.x | Visual Studio 2019 |
| 2.10.0 | Visual Studio 2017 バージョン 15.9 |
| 2.9.0 | Visual Studio 2017 バージョン 15.8 |
| 2.8.2 | Visual Studio 2017 バージョン 15.7 |
| 2.7.0 | Visual Studio 2017 バージョン 15.6 |
| 2.6.1 | Visual Studio 2017 バージョン 15.5 |
| 2.4.0 | Visual Studio 2017 バージョン 15.4 |
| 2.3.2 | Visual Studio 2017 バージョン 15.3 |
| 2.2.0 | Visual Studio 2017 バージョン 15.2 |
| 2.1.0 | Visual Studio 2017 バージョン 15.1 |
| 2.0.0 | Visual Studio 2017 RTM |
| 1.3.2 | Visual Studio 2015 更新プログラム3 |
| 1.2.2 | Visual Studio 2015 更新プログラム2 |
| 1.1.1 | Visual Studio 2015 更新プログラム1 |
| 1.0.1 | Visual Studio 2015 RTM |

> [!TIP]
> サポートされている Visual Studio の最小バージョンが Visual Studio 2017 バージョンである Roslyn パッケージの場合、Visual Studio 2019 のすべてのバージョンは、後で提供されているため、すべてサポートされています。

## <a name="see-also"></a>関連項目

- [.NET Compiler Platform SDK](/dotnet/csharp/roslyn-sdk/)
- [Roslyn アナライザーを使ってみる](getting-started-with-roslyn-analyzers.md)
