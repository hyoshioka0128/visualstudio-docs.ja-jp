---
description: 多数の .NET メモリ オブジェクトが、ジェネレーション 2 のガベージ コレクションで回収されています。
title: DA0005 - 頻繁な GC2 のコレクションです | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0005
- vs.performance.rules.DAManyGC2Collections
- vs.performance.5
- vs.performance.rules.DA0005
ms.assetid: 8d3f267c-8a74-4cf4-91a5-0b06a76dc2bd
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 73b24eba94791a9a24b80898fb7333665ed13caf
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221029"
---
# <a name="da0005-frequent-gc2-collections"></a>DA0005:GC2 のコレクションが頻繁です

|アイテム|[値]|
|-|-|
|規則 ID|DA0005|
|カテゴリ|.NET Framework の使用|
|プロファイル方法|.NET メモリ|
|メッセージ|オブジェクトの多くはジェネレーション 2 のガベージ コレクションで収集されています。|
|メッセージの種類|警告|

## <a name="cause"></a>原因
 多数の .NET メモリ オブジェクトが、ジェネレーション 2 のガベージ コレクションで回収されています。

## <a name="rule-description"></a>規則の説明
 Microsoft .NET 共通言語ランタイム (CLR: Common Language Runtime) は、自動メモリ管理メカニズムを備えています。このメカニズムでは、ガベージ コレクターを使用して、アプリケーションが使用しなくなったオブジェクトのメモリを解放します。 ガベージ コレクターはジェネレーション指向です。これは、多くの割り当てが短時間で終了することを前提としています。 たとえば、ローカル変数の有効期間は短時間です。 新しく作成されたオブジェクトはジェネレーション 0 (gen 0) から始まり、ガベージ コレクションの実行中に破棄されなければジェネレーション 1 に昇格します。その後もアプリケーションによって引き続き使用されていれば、最後はジェネレーション 2 に昇格します。

 ジェネレーション 0 のオブジェクトの収集頻度は高く、通常は非常に効率的に収集されます。 ジェネレーション 1 のオブジェクトの収集頻度はそれよりも低くなり、収集効率も下がります。 有効期間の長いジェネレーション 2 のオブジェクトの場合、収集頻度はさらに低くなります。 また、ジェネレーション 2 のコレクション (フル ガベージ コレクションの実行) は、最も負荷のかかる操作になります。

 この規則は、ジェネレーション 2 のガベージ コレクションの発生率が高くなりすぎた場合に適用されます。 有効期間が比較的短いオブジェクトの多くが、ジェネレーション 1 のコレクションでは収集されずにジェネレーション 2 のコレクションで収集される場合、メモリ管理のコストが簡単に高くなる可能性があります。 詳細については、MSDN Web サイトの「Rico Mariani's Performance Tidbits」 (Rico Mariani のパフォーマンスに関する話題) の「[Mid-life crisis](/archive/blogs/ricom/mid-life-crisis)」 (有効期間半ばでの危機) の投稿を参照してください。

## <a name="how-to-investigate-a-warning"></a>警告の調査方法
 [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md) レポートを確認して、メモリ割り当てに関するアプリケーションのパターンを把握します。 [オブジェクトの有効期間ビュー](../profiling/object-lifetime-view.md)を使用して、ジェネレーション 2 に残っており、その後そこから解放される、プログラムのデータ オブジェクトを確認します。 [割り当てビュー](../profiling/dotnet-memory-allocations-view.md)を使用して、これらの割り当てが行われた実行パスを判断します。

 ガベージ コレクションのパフォーマンスの向上の方法の詳細については、Microsoft Web サイトの「[ガベージ コレクターの基本とパフォーマンスのヒント](/previous-versions/dotnet/articles/ms973837(v=msdn.10))」を参照してください。 自動ガベージ コレクションのオーバーヘッドについては、「[Large Object Heap Uncovered](/archive/msdn-magazine/2008/june/clr-inside-out-large-object-heap-uncovered)」 (大きなオブジェクト ヒープの秘密) を参照してください。
