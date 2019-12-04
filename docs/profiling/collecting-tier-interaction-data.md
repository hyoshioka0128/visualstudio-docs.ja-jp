---
title: 階層相互作用データの収集 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.tierinteraction
helpviewer_keywords:
- Profiling Tools,ADO.NET profiling
- tier interaction profiling method
- Profiling Tools,tier-interaction method
- ADO.NET performance profiling
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e01259fdd23e60a1408addc10a6af3a12479c9f2
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74772819"
---
# <a name="collect-tier-interaction-data"></a>階層相互作用データを収集する

階層相互作用プロファイリングにより、ADO.NET サービスを通じてデータベースと通信する多階層アプリケーションの関数の実行時間に関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。

**Visual Studio のエディション**

階層相互作用プロファイル データは、Visual Studio の任意のエディションを使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、Visual Studio Enterprise のみです。

**Windows 8 と Windows Server 2012**

Windows 8 デスクトップ アプリおよび Windows Server 2012 アプリで階層相互作用データを収集するには、インストルメンテーション メソッドを使用する必要があります。 UWP アプリの階層相互作用データを収集することはできません。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。 階層相互作用データは、サポートされている他のバージョンの Windows で、すべてのプロファイル方法に含めることができます。

**パフォーマンス ウィザード**

パフォーマンス ウィザードのバグのため、パフォーマンス エクスプローラーから、階層相互作用データの収集オプションをプロファイリング実行に追加する必要があります。 また、パフォーマンス エクスプローラーのターゲット ノードに、プロジェクト、実行可能ファイル、または Web サイトを追加する必要があります。

## <a name="to-add-tier-interaction-data-to-a-profiling-run-by-using-the-performance-session-property-pages"></a>パフォーマンス セッションのプロパティ ページを使用して実行されるプロファイリングに階層相互作用データを追加するには

1. パフォーマンス エクスプローラーで、コンテキスト メニューの **[プロパティ]** をクリックします。

2. **[階層の相互作用]** ページを選択し、 **[階層の相互作用のプロファイルを有効にする]** チェック ボックスをオンにします。

3. パフォーマンス エクスプローラーで、 **[ターゲット]** ノードを選択し、プロファイリングするプロジェクト、実行可能ファイル、または Web サイトを指定します。

## <a name="see-also"></a>関連項目

[階層の相互作用ビュー](../profiling/tier-interactions-view.md)
