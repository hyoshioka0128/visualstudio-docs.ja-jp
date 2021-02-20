---
title: .NET Framework ランタイムを指定する | Microsoft Docs
description: .NET Framework ランタイムのさまざまなバージョンを使用してビルドされたモジュールでアプリケーションを構成するしくみについて学習します。
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Profiling Tools, .NET Framework versions
- .NET Framework versions,profililng
ms.assetid: d39f3579-719a-4f47-a97d-5b4232fe4c64
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: da2a19b702e29589a71e84776fbff939dc468914
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918810"
---
# <a name="how-to-specify-the-net-framework-runtime"></a>方法: .NET Framework ランタイムを指定する

リリース .NET Framework 4 では、アプリケーションは .NET Framework ランタイムのさまざまなバージョンを使用してビルドされたモジュールで構成できます。 既定では、Visual Studio プロファイリング ツールは、アプリケーションによって読み込まれる最初のランタイムをプロファイリングします。 プロファイラーを使用してアプリケーションを開始するときと、既に実行中のアプリケーションにプロファイラーをアタッチするときにランタイムがプロファイリングするよう指定できます。

## <a name="to-specify-the-net-framework-run-time-to-profile-when-starting-an-application-with-the-profiler"></a>プロファイラーを使用したアプリケーションの開始時にプロファイリングする .NET Framework ランタイムを指定するには

1. **パフォーマンス エクスプローラー** で、パフォーマンス セッション名を右クリックして **[プロパティ]** をクリックしてから、 **[詳細]** をクリックします。

     **[ターゲット CLR バージョン]** 一覧ボックスに **[自動]** およびコンピューターにインストールされている .NET Framework ランタイムのバージョンが表示されます。

2. 次のいずれかの操作を実行します。

    - プロファイリングする CLR のバージョンをクリックします。

    - **[自動]** をクリックして、アプリケーションが最初に読み込んだバージョンをプロファイルします。

## <a name="to-specify-the-net-framework-run-time-to-profile-when-attaching-the-profiler-to-an-application"></a>アプリケーションにプロファイラーをアタッチするときにプロファイリングする .NET Framework ランタイムを指定するには

1. **[分析]** メニューの **[プロファイラー]** をポイントし、 **[アタッチ/デタッチ]** をクリックします。

2. **[プロファイラーのプロセスへのアタッチ]** ダイアログ ボックスで、プロファイリングするプロセスをクリックします。

     **[ターゲット CLR バージョン]** 一覧ボックスに **[自動]** およびコンピューターにインストールされている .NET Framework ランタイムのバージョンが表示されます。

3. 次のいずれかの操作を実行します。

    - プロファイリングする CLR のバージョンをクリックします。

    - **[自動]** をクリックして、プロファイラーがアプリケーションにアタッチされたときに読み込まれたバージョンをプロファイリングします。
