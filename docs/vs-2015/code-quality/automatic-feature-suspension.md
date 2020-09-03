---
title: 自動機能の中断 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b9c80ba76ba2da978c9cb475299ba0fc9e614120
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655144"
---
# <a name="automatic-feature-suspension"></a>自動機能の中断
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
使用可能なシステムメモリが200MB 以下になると、Visual Studio によってコードエディターに次のメッセージが表示されます。

 ![アラートテキストの完全なソリューション分析の中断](../code-quality/media/fsa-alert.png "FSA_Alert")

 Visual Studio はメモリ不足の状態を検出すると、安定した状態を維持するために、特定の高度な機能を自動的に中断します。 この高度な機能の中断の警告が表示された場合、Visual Studio は以前と同様に機能しますが、パフォーマンスは若干低下します。

 メモリ不足の状態では、次の処理が行われます。

- Visual C# および Visual Basic の完全なソリューション分析は無効になっています。

- Visual C# および Visual Basic の[ガベージコレクション](https://msdn.microsoft.com/library/22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9)(GC) の低待機時間モードは無効になっています。

- Visual Studio キャッシュがフラッシュされます。

## <a name="improve-visual-studio-performance"></a>Visual Studio のパフォーマンスの向上
 大規模なソリューションやメモリ不足の状況に対処するときに Visual Studio のパフォーマンスを向上させる方法に関するヒントとテクニックについては、「 [大規模なソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)」を参照してください。

## <a name="full-solution-analysis-suspended"></a>完全なソリューション分析が中断されました
 既定では、完全なソリューション分析は Visual Basic に対して有効になり、Visual C# では無効になります。 ただし、メモリ不足の状態では、[オプション] ダイアログボックスの設定に関係なく、完全なソリューション分析が Visual Basic と Visual C# の両方で自動的に無効になります。 ただし、[オプション] ダイアログボックスの [**完全なソリューション分析を有効にする**] チェックボックスをオンにするか、Visual Studio を再起動して、情報バーに表示されたときに [**再有効化**] ボタンを選択することで、完全なソリューション分析を再び有効にすることができます。 [オプション] ダイアログボックスには、常に現在の完全なソリューション分析の設定が表示されます。 詳細については、「 [方法: 完全なソリューション分析を有効または無効](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)にする」を参照してください。

## <a name="gc-low-latency-disabled"></a>GC 低待機時間の無効化
 GC 低待機時間モードを再度有効にするには、Visual Studio を再起動します。  既定では、入力で GC 操作をブロックしないように入力すると、Visual Studio は GC 低待機時間モードを有効にします。 ただし、メモリ不足の状態が原因で、Visual Studio によって自動中断の警告が表示される場合、そのセッションの GC 低待機時間モードは無効になります。 Visual Studio を再起動すると、既定の GC 動作が再度有効になります。 詳細については、「<xref:System.Runtime.GCLatencyMode>」を参照してください。

## <a name="visual-studio-caches-flushed"></a>フラッシュされる Visual Studio キャッシュ

すべての Visual Studio キャッシュはすぐに空になりますが、現在の開発セッションを続行するか、Visual Studio を再起動すると、再作成が開始されます。 フラッシュされたキャッシュには、次の機能のキャッシュが含まれます。

- [すべての参照の検索]

- [移動]

- Using の追加

また、Visual Studio の内部操作に使用されるキャッシュもクリアされます。

> [!NOTE]
> 自動機能の中断の警告は、セッションごとではなく、ソリューションごとに1回だけ発生します。 つまり、Visual Basic から Visual C# (またはその逆) に切り替えて、別のメモリ不足の状態になった場合、別の自動機能中断警告が表示される可能性があります。

## <a name="see-also"></a>関連項目

- [方法: 完全ソリューション分析を有効/無効にする](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)
- [ガベージ コレクションの基礎](https://msdn.microsoft.com/library/67c5a20d-1be1-4ea7-8a9a-92b0b08658d2)
- [大規模なソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)