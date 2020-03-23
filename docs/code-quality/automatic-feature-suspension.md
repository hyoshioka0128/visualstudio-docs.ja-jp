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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e8480eb57a08905c2a593adbab519ae793638888
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431242"
---
# <a name="automatic-feature-suspension"></a>自動機能の中断

使用可能なシステム メモリが 200 MB 以下になると、Visual Studio では次のメッセージがコード エディターに表示されます。

![完全なソリューション分析を中断するアラート テキスト](../code-quality/media/fsa_alert.png)

Visual Studio はメモリ不足の状態を検出すると、特定の高度な機能を自動的に中断して、安定した状態を維持します。 Visual Studio は以前と同様に動作し続けますが、パフォーマンスが低下します。

メモリ不足の状態では、次のアクションが実行されます。

- Visual C# および Visual Basic のライブ コード分析は、最小限のスコープに縮小されます。

- Visual C# および Visual Basic の[ガベージ コレクション](/dotnet/standard/garbage-collection/index)(GC) の待機時間の短いモードが無効になっています。

- ビジュアル スタジオのキャッシュがフラッシュされます。

## <a name="improve-visual-studio-performance"></a>ビジュアル スタジオのパフォーマンスを向上させる

大規模なソリューションやメモリ不足の状況に対処する場合に Visual Studio のパフォーマンスを向上させるヒントとテクニックについては、「大規模なソリューション[のパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)」を参照してください。

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>ライブ コード分析は最小限のスコープに縮小されます。

既定では、開いているドキュメントおよびプロジェクトに対してライブ コード分析が実行されます。 この分析範囲をカスタマイズして、現在のドキュメントに縮小したり、ソリューション全体にまで拡大したりできます。 詳細については、「[方法 : マネージ コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。 メモリ不足の状態では、Visual Studio は、現在のドキュメントにライブ分析スコープを減らします。 ただし、表示されたら情報バーの [**再有効化**] ボタンを選択するか、Visual Studio を再起動することで、優先分析スコープを再度有効にできます。 [オプション] ダイアログ ボックスには、現在のライブ コード分析スコープの設定が常に表示されます。

## <a name="gc-low-latency-disabled"></a>GC の低遅延が無効

GC の待機時間の短いモードを再度有効にするには、Visual Studio を再起動します。 既定では、入力時に GC の待機時間が短いモードが有効になり、入力によって GC 操作がブロックされないようになります。 ただし、メモリ不足の状態で Visual Studio が自動中断の警告を表示する場合、GC の低待機時間モードはそのセッションで無効になります。 Visual Studio を再起動すると、既定の GC 動作が再度有効になります。 詳細については、<xref:System.Runtime.GCLatencyMode> を参照してください。

## <a name="visual-studio-caches-flushed"></a>フラッシュされたビジュアル スタジオ のキャッシュ

現在の開発セッションを続行するか、Visual Studio を再起動すると、すべての Visual Studio キャッシュはすぐに空になりますが、再設定が開始されます。 フラッシュされたキャッシュには、次の機能のキャッシュが含まれます。

- [すべての参照の検索]

- [移動]

- 使用を追加

さらに、内部の Visual Studio 操作に使用されるキャッシュもクリアされます。

> [!NOTE]
> 自動機能停止警告は、ソリューションごとに 1 回だけ発生し、セッション単位では発生しません。 つまり、Visual Basic から Visual C# に切り替えて (またはその逆)、別のメモリ不足状態に陥った場合、機能の中断が自動的に発生する可能性があります。

## <a name="see-also"></a>関連項目

- [方法: マネージ コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)
- [ガベージ コレクションの基礎](/dotnet/standard/garbage-collection/fundamentals)
- [大規模ソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)
