---
title: レガシコード分析を無効にする
ms.date: 10/04/2019
description: Visual Studio でバイナリコード分析をオンまたはオフにする方法について説明します。 「マネージコードプロジェクトでこの機能を構成する方法」を参照してください。
ms.custom: SEO-VS-2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: c10aa602c2c9af3c51812073d62d5bd9bff06664
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860075"
---
# <a name="how-to-enable-and-disable-binary-code-analysis-for-managed-code"></a>方法: マネージコードのバイナリコード分析を有効または無効にする

マネージコードプロジェクトの各ビルドの後に実行するように、レガシコード分析 (バイナリ分析) を構成できます。 また、デバッグやリリースなど、ビルド構成ごとに異なる設定を使用することもできます。

> [!NOTE]
> レガシ分析は、.NET Core や .NET Standard アプリなどの新しいプロジェクトの種類では使用できません。 これらのプロジェクトでは、 [.NET Compiler Platform ベースのコードアナライザー](roslyn-analyzers-overview.md) を使用して、コードをライブとビルド時の両方で分析します。 これらのプロジェクトでソースコード分析を無効にする方法の詳細については、「 [ソースコード分析を無効にする方法](disable-code-analysis.md)」を参照してください。

レガシコード分析を有効または無効にするには:

1. **ソリューションエクスプローラー** で、プロジェクトを選択して保持 (または右クリック) し、[**プロパティ**] を選択します。

2. プロジェクトの [プロパティ] ダイアログボックスで、[ **コード分析** ] タブにアクセスします。

3. [ **構成** ] でビルドの種類を指定し、[ **プラットフォーム**] でターゲットプラットフォームを指定します。 (Non-.NET Core/.NET Standard プロジェクトのみ。)

::: moniker range="vs-2017"

4. 自動コード分析を有効または無効にするには、[ **ビルド時にコード分析を有効に** する] チェックボックスをオンまたはオフにします。

::: moniker-end

::: moniker range=">=vs-2019"

4. 自動コード分析を有効または無効にするには、[**バイナリアナライザー** ] セクションの [**ビルド時に実行**] チェックボックスをオンまたはオフにします。

   ![Visual Studio でのビルドオプションでのバイナリコード分析の実行](media/run-on-build-binary-analyzers.png)

::: moniker-end

> [!NOTE]
> ビルドでバイナリコード分析を無効にしても、 [.NET Compiler Platform ベースのコードアナライザー](roslyn-analyzers-overview.md)には影響しません。これは、NuGet パッケージとしてインストールした場合、常にビルドで実行されます。 これらのアナライザーからの分析を無効にする方法については、「 [ソースコード分析を無効にする方法](disable-code-analysis.md)」を参照してください。
