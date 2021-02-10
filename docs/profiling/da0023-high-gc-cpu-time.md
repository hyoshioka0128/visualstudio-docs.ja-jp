---
title: DA0023 - 高い GC CPU 時間 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0023
- vs.performance.23
- vs.performance.rules.DA0023
ms.assetid: aba875fe-9cbc-418d-a2c4-6eb47519a5bb
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f719cf2e416e3cb1a58a279d6327810c71e41d0e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99966982"
---
# <a name="da0023-high-gc-cpu-time"></a>DA0023:高い GC CPU 時間

|アイテム|[値]|
|-|-|
|規則 ID|DA0023|
|カテゴリ|.NET Framework の使用|
|プロファイル方法|すべて|
|メッセージ|% Time in GC がかなり高いです。 アプリケーションの応答に、示唆されている過剰なガベージ コレクションのオーバーヘッドが影響している可能性があります。 .NET のメモリ割り当てデータとオブジェクト ライフタイム情報を収集することで、アプリケーションが使用しているメモリ割り当てのパターンを知ることができます。|
|規則の種類|情報|

 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。

## <a name="cause"></a>原因
 プロファイリングの間に収集されたシステム パフォーマンス データで、ガベージ コレクションに費やされた時間がアプリケーション処理時間全体と比較して大きいことが示されています。

## <a name="rule-description"></a>規則の説明
 Microsoft .NET 共通言語ランタイム (CLR: Common Language Runtime) は、自動メモリ管理メカニズムを備えています。このメカニズムでは、ガベージ コレクターを使用して、アプリケーションが使用しなくなったオブジェクトのメモリを解放します。 ガベージ コレクターはジェネレーション指向です。これは、多くの割り当てが短時間で終了することを前提としています。 たとえば、ローカル変数の有効期間は短時間です。 新しく作成されたオブジェクトはジェネレーション 0 (gen 0) から始まり、ガベージ コレクションの実行中に破棄されなければジェネレーション 1 に昇格します。その後もアプリケーションによって引き続き使用されていれば、最後はジェネレーション 2 に昇格します。

 ジェネレーション 0 のオブジェクトの収集頻度は高く、効率的に収集されます。 ジェネレーション 1 のオブジェクトの収集頻度はそれよりも低くなり、収集効率も下がります。 有効期間の長いジェネレーション 2 のオブジェクトの場合、収集頻度はさらに低くなります。 また、ジェネレーション 2 のコレクション (フル ガベージ コレクションの実行) は、最も負荷のかかる操作になります。

 この規則は、ガベージ コレクションに費やされた時間がアプリケーション処理時間全体と比較して大きい場合、適用されます。

> [!NOTE]
> ガーベジ コレクションに費やされた時間の割合が、アプリケーション全体の処理時間と比較して過度である場合、この規則ではなく、「[DA0024: 過剰な GC CPU 時間](../profiling/da0024-excessive-gc-cpu-time.md)」の警告が適用されます。

## <a name="how-to-investigate-a-warning"></a>警告の調査方法
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、プロファイル データの [[マーク] ビュー](../profiling/marks-view.md)に移動します。 **.NET CLR Memory\\% Time in GC** 列を探します。 マネージド メモリのガベージ コレクションが他のフェーズよりも多い特定のプログラム実行フェーズがあるかどうかを確認します。 % Time in GC の値と、 **# of Gen 0 Collections**、 **# of Gen 1 Collections**、 **# of Gen 2 Collections** 値で報告されているガベージ コレクションの割合を比較してください。

 % Time in GC 値は、アプリケーションの処理時間全体に占めるガベージ コレクションの実行時間を報告します。 % Time in GC 値が高くても、それが過度なガベージ コレクションのためではない場合もあることに注意してください。 % Time in GC 値の計算方法の詳細については、MSDN の「**Maoni's Weblog**」 (Maoni のブログ) の「[Difference Between Perf Data Reported by Different Tools - 4](https://devblogs.microsoft.com/maoni/archive/difference-between-perf-data-reported-by-different-tools-4.aspx)」 (ツールによってレポートされるパフォーマンス データの違い - 4) を参照してください。 ページ フォールトが発生している場合や、コンピューター上の優先順位の高い処理のためにアプリケーションに割り込みが発生している場合、% Time in GC カウンターにはそれらの遅延が反映されます。
