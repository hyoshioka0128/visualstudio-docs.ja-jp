---
title: 自動機能の中断
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 236a95cd8d4af8da91199bf79e7c9fe3aa0d49af
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769480"
---
# <a name="automatic-feature-suspension"></a>自動機能の中断

使用可能なシステムメモリが 200 MB 以下になると、Visual Studio によってコードエディターに次のメッセージが表示されます。

![アラートテキストの完全なソリューション分析の中断](../code-quality/media/fsa_alert.png)

Visual Studio はメモリ不足の状態を検出すると、安定した状態を維持するために、特定の高度な機能を自動的に中断します。 Visual Studio は以前と同様に機能しますが、パフォーマンスは低下します。

メモリ不足の状態では、次の操作が行われます。

- Visual C# と Visual Basic のライブコード分析は、最小限のスコープに縮小されます。

- Visual C# および Visual Basic の[ガベージコレクション](/dotnet/standard/garbage-collection/index)(GC) の低待機時間モードは無効になっています。

- Visual Studio キャッシュがフラッシュされます。

## <a name="improve-visual-studio-performance"></a>Visual Studio のパフォーマンスの向上

大規模なソリューションやメモリ不足の状況に対処するときに Visual Studio のパフォーマンスを向上させる方法に関するヒントとテクニックについては、「[大規模なソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)」を参照してください。

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>ライブコード分析が最小スコープに縮小される

既定では、開いているドキュメントとプロジェクトに対してライブコード分析が実行されます。 この分析スコープをカスタマイズして、現在のドキュメントに縮小することも、ソリューション全体に拡張することもできます。 詳細については、「[方法: マネージコードのライブコード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。 メモリ不足の状態では、Visual Studio によってライブ分析のスコープが現在のドキュメントに強制的に縮小されます。 ただし、必要な分析スコープを再び有効にするには、情報バーの表示時に [**再有効化**] ボタンを選択するか、Visual Studio を再起動します。 [オプション] ダイアログボックスには、常に現在のライブコード分析のスコープ設定が表示されます。

## <a name="gc-low-latency-disabled"></a>GC 低待機時間の無効化

GC 低待機時間モードを再度有効にするには、Visual Studio を再起動します。 既定では、入力で GC 操作をブロックしないように入力すると、Visual Studio は GC 低待機時間モードを有効にします。 ただし、メモリ不足の状態が原因で、Visual Studio によって自動中断の警告が表示される場合、そのセッションの GC 低待機時間モードは無効になります。 Visual Studio を再起動すると、既定の GC 動作が有効になります。 詳細については、「<xref:System.Runtime.GCLatencyMode>」を参照してください。

## <a name="visual-studio-caches-flushed"></a>フラッシュされる Visual Studio キャッシュ

現在の開発セッションを続行するか、Visual Studio を再起動すると、すべての Visual Studio キャッシュがすぐに空になり、再作成が開始されます。 フラッシュされるキャッシュには、次の機能のキャッシュが含まれます。

- [すべての参照の検索]

- [移動]

- Using の追加

また、Visual Studio の内部操作に使用されるキャッシュもクリアされます。

> [!NOTE]
> 自動機能の中断の警告は、セッションごとではなく、ソリューションごとに1回だけ発生します。 つまり、Visual Basic から Visual C# (またはその逆) に切り替えて、別のメモリ不足の状態になった場合、別の自動機能中断警告が表示される可能性があります。

## <a name="see-also"></a>関連項目

- [方法: マネージコードのライブコード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)
- [ガベージ コレクションの基礎](/dotnet/standard/garbage-collection/fundamentals)
- [大規模なソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)
