---
title: '方法: .NET Framework ランタイムを指定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, .NET Framework versions
- .NET Framework versions,profililng
ms.assetid: d39f3579-719a-4f47-a97d-5b4232fe4c64
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2f631e8639c1004fa2cb005da3b6c8bcb27f1a9b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203402"
---
# <a name="how-to-specify-the-net-framework-runtime"></a>方法: .NET Framework ランタイムを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リリース [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)] では、アプリケーションは [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ランタイムのさまざまなバージョンを使用してビルドされたモジュールで構成できます。 既定では、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールは、アプリケーションによって読み込まれる最初のランタイムをプロファイリングします。 プロファイラーを使用してアプリケーションを開始するときと、既に実行中のアプリケーションにプロファイラーをアタッチするときにランタイムがプロファイリングするよう指定できます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
### <a name="to-specify-the-net-framework-run-time-to-profile-when-starting-an-application-with-the-profiler"></a>プロファイラーを使用したアプリケーションの開始時にプロファイリングする .NET Framework ランタイムを指定するには  
  
1. **パフォーマンス エクスプローラー**で、パフォーマンス セッション名を右クリックして **[プロパティ]** をクリックしてから、 **[詳細]** をクリックします。  
  
     **[ターゲット CLR バージョン]** 一覧ボックスに **[自動]** およびコンピューターにインストールされている [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ランタイムのバージョンが表示されます。  
  
2. 次のいずれかの操作を実行します。  
  
    - プロファイリングする CLR のバージョンをクリックします。  
  
    - **[自動]** をクリックして、アプリケーションが最初に読み込んだバージョンをプロファイルします。  
  
### <a name="to-specify-the-net-framework-run-time-to-profile-when-attaching-the-profiler-to-an-application"></a>アプリケーションにプロファイラーをアタッチするときにプロファイリングする .NET Framework ランタイムを指定するには  
  
1. [分析] メニューの [プロファイラー] をポイントし、[アタッチ/デタッチ] をクリックします。  
  
2. [プロファイラーのプロセスへのアタッチ] ダイアログ ボックスで、プロファイリングするプロセスをクリックします。  
  
     **[ターゲット CLR バージョン]** 一覧ボックスに **[自動]** およびコンピューターにインストールされている [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ランタイムのバージョンが表示されます。  
  
3. 次のいずれかの操作を実行します。  
  
    - プロファイリングする CLR のバージョンをクリックします。  
  
    - **[自動]** をクリックして、プロファイラーがアプリケーションにアタッチされたときに読み込まれたバージョンをプロファイリングします。
