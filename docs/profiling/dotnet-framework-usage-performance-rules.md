---
title: .NET Framework の使用に関するパフォーマンス規則 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ab573755-6370-48aa-853d-a7321c424c79
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5a740885d8876398bf86e279aa259e9169fcf7c2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779288"
---
# <a name="net-framework-usage-performance-rules"></a>.NET Framework の使用に関するパフォーマンス規則
.NET Framework の使用カテゴリのパフォーマンス規則では、最適化できる具体的なメソッド、およびパフォーマンスに問題があるときに調査できる一般的な使用パターン (ガベージ コレクションやロックの競合など) が示されています。

|||
|-|-|
|[DA0001: StringBuilder を使用して連結してください](../profiling/da0001-use-stringbuilder-for-concatenations.md)|<xref:System.String.Concat(System.String,System.String)?displayProperty=fullName> の呼び出しがプロファイル データの大きな割合を占めています。 <xref:System.Text.StringBuilder> クラスを使用して、複数のセグメントからの文字列を連結することを検討してください。|
|[DA0005: 頻繁な GC2 のコレクションです](../profiling/da0005-frequent-gc2-collections.md)|比較的多数の .NET メモリ オブジェクトが、ジェネレーション 2 のガベージ コレクションで回収されています。 ジェネレーション 1 のコレクションで回収されない有効期間の短いオブジェクトが多すぎる場合、メモリ管理コストが簡単に過剰になる可能性があります。|
|[DA0006: 値の型で Equals() をオーバーライドしてください](../profiling/da0006-override-equals-parens-for-value-types.md)|パブリック値型の `Equals` メソッドまたは等値演算子の呼び出しが、プロファイリング データの大きな割合を占めています。 さらに効率的な方法を実装することを検討してください。|
|[DA0007: 制御フローでの例外の使用を避けてください](../profiling/da0007-avoid-using-exceptions-for-control-flow.md)|.NET Framework 例外ハンドラーの多くの部分が、プロファイリング データで呼び出されました。 他の制御フロー ロジックを使用して、スローされる例外の数を減らすことを検討してください。|
|[DA0010: GetHashCode の負荷が高くなっています](../profiling/da0010-expensive-gethashcode.md)|型の `GetHashCode` メソッドの呼び出しがプロファイリング データの大きな割合を占めているか、または `GetHashCode` メソッドがメモリを割り当てています。 メソッドの複雑さを軽減してください。|
|[DA0011: CompareTo の負荷が高くなっています](../profiling/da0011-expensive-compareto.md)|型の `CompareTo` メソッドが高コストであるか、またはメソッドがメモリを割り当てています。 `CompareTo` メソッドの複雑さを軽減してください。|
|[DA0012: リフレクションが頻繁に実行されています](../profiling/da0012-significant-amount-of-reflection.md)|<xref:System.Reflection.IReflect.InvokeMember%2A> や <xref:System.Reflection.IReflect.GetMember%2A> など、<xref:System.Reflection?displayProperty=fullName> メソッドの呼び出しか、<xref:System.Type.InvokeMember%2A> など、Type メソッドの呼び出しがプロファイリング データの大きな割合を占めています。 可能な場合は、事前バインディングを使用するこれらのメソッドを、依存アセンブリのメソッドに置き換えることを検討してください。|
|[DA0013: String.Split/String.Substring が頻繁に使用されています](../profiling/da0013-high-usage-of-string-split-or-string-substring.md)|<xref:System.String.Split%2A?displayProperty=fullName> メソッドまたは <xref:System.String.Substring%2A> メソッドの呼び出しがプロファイリング データの大きな割合を占めています。 文字列内の部分文字列の存在をテストしている場合、<xref:System.String.IndexOf%2A> または <xref:System.String.IndexOfAny%2A> の利用を検討してください。|
|[DA0018: 32 ビット アプリケーションがプロセスのマネージド メモリ制限で実行されています](../profiling/da0018-32-bit-application-running-at-process-managed-memory-limits.md)|プロファイリングの実行中に収集されたシステム データで、.NET Framework のメモリ ヒープが、32 ビット プロセスでマネージド ヒープが到達可能な最大サイズに近づいたことが示されています。 .NET メモリ プロファイル方法を使って再度プロファイリングを行い、アプリケーションによるマネージド リソースの使用を最適化することを検討してください。|
|[DA0021: ジェネレーション 1 のガベージ コレクションが高率です](../profiling/da0021-high-rate-of-gen-1-garbage-collections.md)|比較的多数の .NET メモリ オブジェクトが、ジェネレーション 1 のガベージ コレクションで回収されています。 ジェネレーション 0 のコレクションで回収されない有効期間の短いオブジェクトが多すぎる場合、メモリ管理コストが簡単に過剰になる可能性があります。|
|[DA0022: ジェネレーション 2 のガベージ コレクションが高率です](../profiling/da0022-high-rate-of-gen-2-garbage-collections.md)|多数の .NET メモリ オブジェクトが、ジェネレーション 2 のガベージ コレクションで回収されています。 ジェネレーション 1 のコレクションで回収されない有効期間の短いオブジェクトが多すぎる場合、メモリ管理コストが簡単に過剰になる可能性があります。 このルールは、ロック競合の割合がルール DA0005 の上限しきい値を超えると発生します。|
|[DA0023: 高い GC CPU 時間](../profiling/da0023-high-gc-cpu-time.md)|プロファイリングの間に収集されたシステム パフォーマンス データで、ガベージ コレクションに費やされた時間がアプリケーション処理時間全体と比較して大きいことが示されています。|
|[DA0024: 過剰な GC CPU 時間](../profiling/da0024-excessive-gc-cpu-time.md)|プロファイリングの間に収集されたシステム パフォーマンス データで、ガベージ コレクションに費やされた時間がアプリケーション処理時間全体と比較して大き過ぎることが示されています。 このルールは、ガベージ コレクションに費やされた時間がルール DA0023 の上限しきい値を超えると発生します。|
|[DA0038: 高率のロック競合](../profiling/da0038-high-rate-of-lock-contentions.md)|プロファイリング データで収集されたシステム パフォーマンス データが、アプリケーションの実行中に非常に高率のロック競合が発生したことを示しています。 競合の原因を見つけるために、コンカレンシー プロファイル方法を使用して、プロファイリングを再度実行することを検討してください。|
|[DA0039: 非常に高率のロック競合](../profiling/da0039-very-high-rate-of-lock-contentions.md)|プロファイリング データで収集されたシステム パフォーマンス データが、アプリケーションの実行中に極端に高率のロック競合が発生したことを示しています。 競合の原因を見つけるために、コンカレンシー プロファイル方法を使用して、プロファイリングを再度実行することを検討してください。 このルールは、ロック競合の割合がルール DA0038 の上限しきい値を超えると発生します。|
