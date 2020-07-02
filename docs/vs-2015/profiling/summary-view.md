---
title: 概要ビュー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.summary
helpviewer_keywords:
- performance reports, summary view
- profiling tools reports, Summary view
- profiling tools, Summary view
- Summary view
ms.assetid: 98a1eb71-bbf5-4ce7-8559-cdc29f082c4b
caps.latest.revision: 42
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f4346b0e7459ee3c78669ab9178555370ffac16d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545510"
---
# <a name="summary-view"></a>概要 ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

概要ビューには、プロファイル実行で最もパフォーマンスに負荷のかかる関数またはオブジェクトに関する情報が表示されます。 このビューには、タイムライン グラフと、プロファイル方法のパフォーマンス メトリックスに基づいて最も負荷のかかる関数またはオブジェクトの 2 つ以上の一覧が表示されます。 このビュー内のデータは、使用されたプロファイル方法 (サンプリング、インストルメンテーション、またはコンカレンシー) および .NET メモリ割り当てを収集対象としたかどうかによって異なります。  
  
 コンカレンシー データの概要ビューを除くすべての概要ビューでは、概要ビューのタイムライン グラフに、プロファイリングが行われた期間のプロファイリングされたアプリケーションのプロセッサ (CPU) 使用率が表示されます。  
  
- グラフ上の時間セグメントを指定する場合、そのセグメントのデータを再分析したり、タイムライン表示で指定したセグメントをズーム表示することができます。 詳細については、「[方法: 概要のタイムラインからレポートビューをフィルター処理する](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)」を参照してください。  
  
- 概要ビュー リストの関数をクリックして、その関数の [関数の詳細] ビューを開くことができます。 また、他のビュー オプションの関数を右クリックすることもできます。  
  
- 概要ビュー リストに表示される項目の数を変更するには、 **[ツール]** メニューを開き、 **[オプション]** をポイントし、 **[パフォーマンス ツール]** をクリックします。 **[全般設定]** で、 **[概要ビュー内の関数の数]** 設定を変更します。  
  
## <a name="notifications-links"></a>通知リンク  
 通知リストのリンクをクリックして、レポートの表示オプションを設定できます。 このリストはタイムライン グラフの右側に表示されます。  
  
|オプション|説明|  
|-|-|  
|**Show Non-User Code (非ユーザー コードの表示)**<br /><br /> **マイ コードのみ表示**|ネイティブ コード、またはインストルメンテーション メソッドを使用して収集されたプロファイル データには使用できません。 ユーザー コードからのデータのみの表示 ( **[マイ コードのみ表示]** ) と、システム コードを含むすべてのコードからのデータの表示 ( **[Show Non-User Code] (非ユーザー コードの表示)** ) を切り替えます。 既定では、データはユーザー コードに制限されます。 設定を変更するには、「[方法: レポートビューをフィルタープロファイルツール処理してマイコードのみを表示](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md)する」を参照してください。|  
|**ガイダンスの表示**|パフォーマンス規則の警告を **[エラー一覧]** ウィンドウに表示します。 詳細については、「[パフォーマンス規則を使用したデータの分析](../profiling/using-performance-rules-to-analyze-data.md)」を参照してください。|  
  
## <a name="report"></a>レポート  
 レポート リストのリンクをクリックし、別のビューを開いてレポートを表示、比較、保存、またはフィルター処理できます。 このリストはタイムライン グラフの右側に表示されます。  
  
|名前|説明|  
|-|-|  
|**トリミングされたコール ツリーの表示**|コール ツリー ビューに最も負荷が高い実行パスを表示します。 詳細については、「[コールツリービュー](../profiling/call-tree-view.md)」を参照してください。|  
|**ホット ラインの表示**|インストルメンテーション メソッドを使用して収集されたプロファイル データには使用できません。 行ビューに最も負荷が高いソース コードを表示します。 詳細については、「[行ビュー](../profiling/lines-view.md)」を参照してください。|  
|**レポートの比較**|**[比較のための分析ファイルを選択します]** ダイアログ ボックスを表示します。このダイアログ ボックスで、現在のファイルと比較する別のプロファイル データ ファイルを指定できます。 詳細については、「[パフォーマンス データ ファイルの比較](../profiling/comparing-performance-data-files.md)」を参照してください。|  
|**レポート データのエクスポート**|**[レポートのエクスポート]** ダイアログ ボックスを表示します。このダイアログ ボックスで、コンマ区切りの値 (.csv) または .xml ファイルとして保存する 1 つ以上のレポート ビューを指定できます。 詳細については、「[方法: プロファイルツールレポートをエクスポートする](https://msdn.microsoft.com/174b5bd3-df9b-4fd4-88d4-76032ab90451)」を参照してください。|  
|**分析されたレポートの保存**|現在のプロファイル データ ファイルを .vsps ファイルとして保存します。このファイルは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインターフェイスでよりすばやく開くことができます。 詳細については、「[方法: 分析されたプロファイリングデータファイルを保存する](https://msdn.microsoft.com/0340ddde-caf4-48ac-8af3-d15dcdade556)」を参照してください。|  
|**レポート データのフィルター**|プロファイル レポート フィルター ウィンドウを表示します。このウィンドウでは、レポート ビューに表示されるデータを制限するための条件を指定できます。 詳細については、「[パフォーマンスレポートビューフィルター](../profiling/performance-report-view-filter.md) 」を参照してください。|  
|**全画面表示の切り替え**|レポート ビューの全画面表示モードを切り替えます。|  
  
## <a name="see-also"></a>関連項目  
 [概要ビュー](../profiling/summary-view-sampling-data.md)   
 [概要ビュー](../profiling/summary-view-instrumentation-data.md)   
 [概要ビュー](../profiling/summary-view-dotnet-memory-data.md)
