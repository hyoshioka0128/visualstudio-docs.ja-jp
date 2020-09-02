---
title: 階層相互作用データの収集 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.tierinteraction
helpviewer_keywords:
- Profiling Tools,ADO.NET profiling
- tier interaction profiling method
- Profiling Tools,tier-interaction method
- ADO.NET performance profiling
ms.assetid: 47a944c2-3098-497c-8fc7-e1f43d750bbc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a20266c870316be9b6be67e661d13eb4e6fdbaee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62568048"
---
# <a name="collecting-tier-interaction-data"></a>階層相互作用データの収集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

階層相互作用プロファイリングにより、ADO.NET サービスを通じてデータベースと通信する多階層アプリケーションの関数の実行時間に関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。  
  
 **Visual Studio のエディション**  
  
 階層相互作用プロファイル データは、Visual Studio Ultimate、Visual Studio Premium、または Visual Studio Professional を使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、VS Ultimate および VS Premium のみです。  
  
 **Windows 8 と Windows Server 2012**  
  
 Windows 8 デスクトップ アプリおよび Windows Server 2012 アプリで階層相互作用データを収集するには、インストルメンテーション メソッドを使用する必要があります。 Windows ストア アプリの階層相互作用データを収集することはできません。 ｢[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。 階層相互作用データは、サポートされている他のバージョンの Windows で、すべてのプロファイル方法に含めることができます。  
  
 **パフォーマンス ウィザード**  
  
 パフォーマンス ウィザードのバグのため、パフォーマンス エクスプローラーから、階層相互作用データの収集オプションをプロファイリング実行に追加する必要があります。 また、パフォーマンス エクスプローラーのターゲット ノードに、プロジェクト、実行可能ファイル、または Web サイトを追加する必要があります。  
  
### <a name="to-add-tier-interaction-data-to-a-profiling-run-by-using-the-performance-session-property-pages"></a>パフォーマンス セッションのプロパティ ページを使用して実行されるプロファイリングに階層相互作用データを追加するには  
  
1. パフォーマンス エクスプローラーで、コンテキスト メニューの **[プロパティ]** をクリックします。  
  
2. **[階層の相互作用]** ページを選択し、 **[階層の相互作用のプロファイルを有効にする]** チェック ボックスをオンにします。  
  
3. パフォーマンス エクスプローラーで、 **[ターゲット]** ノードを選択し、プロファイリングするプロジェクト、実行可能ファイル、または Web サイトを指定します。  
  
## <a name="see-also"></a>参照  
 [階層の相互作用ビュー](../profiling/tier-interactions-view.md)
