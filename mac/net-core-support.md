---
title: .NET Core サポート
description: このドキュメントでは、Visual Studio for Mac の .NET Core バージョンのサポートについて説明します
author: sayedihashimi
ms.author: sayedha
ms.date: 01/08/2020
ms.assetid: 8B8CEBE8-00DA-4AD1-8193-77F58B57F244
ms.openlocfilehash: 4009e6c139ef33bcd4caa01a9313695628757884
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91583932"
---
# <a name="net-core-support"></a>.NET Core サポート

次の表では、Visual Studio for Mac の安定およびプレビュー バージョンによってサポートされている .NET Core のバージョンについて説明します。

| .NET Core SDK Version |Visual Studio for Mac 8.1 | Visual Studio for Mac 8.2 | Visual Studio for Mac 8.3 | Visual Studio for Mac 8.4 | Visual Studio for Mac 8.5 | Visual Studio for Mac 8.6 |
|---------|---------|---------|---------|---------|---------|---------|
|v2.1.0 - v2.1.5xx | | | | | | |
|v2.1.600 + |✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|
|v2.2.1 - v2.2.1xx | | | | | | |
|v2.2.200 + |✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|
|v3.0 | | |✔︎|✔︎|✔︎|✔︎|
|v3.1 | | | |✔︎|✔︎|✔︎|
|v5.0 (プレビュー) | | | | | |✔︎|

> [!IMPORTANT]
> .NET Core SDK のプレビュー バージョンはサポートされていません。リリース バージョンに更新してください。 Visual Studio for Mac 8.4 をインストールすると、.NET Core v3.1 のリリース バージョンがインストールされます。

> [!IMPORTANT]
> 以前に Visual Studio for Mac 8.0 で .NET Core v2.2.1xx を使用していた場合は、上の表にある .NET Core のサポートされているバージョンに手動で更新する必要があります。 [2.1.700](https://dotnet.microsoft.com/download/dotnet-core/2.1) または [2.2.300](https://dotnet.microsoft.com/download/dotnet-core/2.2) のどちらかをお勧めします

* 8\.4、8.5、8.6 の場合、.NET Core v3.1 が既定でインストールされます。
* 8\.3 の場合、.NET Core v3.0 が既定でインストールされます。
* インストーラーによって、.NET Core v2.1.701 (8.1 用 v2.1.700) が既定でインストールされます。
* .NET Core の他のバージョンをダウンロードするには、[dotnet ページ](https://dotnet.microsoft.com/download/dotnet-core)を参照してください。
* .NET Core 3.0 を使用する場合、C# バージョン 8 が既定で使用されます。 C#7.3 は、.NET Core 2.x を使用する場合の既定です。 詳細については、「[C# 言語のバージョン管理](/dotnet/csharp/language-reference/configure-language-version)」を参照してください。
* プレビュー バージョンの Visual Studio for Mac をインストールする方法について詳しくは、[プレビュー リリースのインストール](./install-preview.md)に関するガイドをご覧ください。