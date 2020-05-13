---
title: マルチプロセッサ環境でのログ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, multi-processor logging
- MSBuild, logging
ms.assetid: dd4dae65-ed04-4883-b48d-59bcb891c4dc
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 35184f6ef724a9f0e803a10c9bda2c6981313ed6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205976"
---
# <a name="logging-in-a-multi-processor-environment"></a>マルチプロセッサ環境でのログ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild では複数のプロセッサを使用できるため、プロジェクトのビルド時間が大幅に短縮されますが、同時にログの複雑性も高まります。 シングルプロセッサ環境であれば、logger は、イベント、メッセージ、警告、およびエラーを順序に従った予測可能な方法で処理できます。 それに対し、マルチプロセッサ環境では、イベントが複数のソースから同時に、または誤った順序で送られてくることがあります。 MSBuild には、マルチプロセッサ対応の新しい logger が用意されており、カスタム "転送 logger" を作成できます。  
  
## <a name="logging-multiple-processor-builds"></a>マルチプロセッサ ビルドのログ  
 1 つ以上のプロジェクトをマルチプロセッサ システムまたはマルチコア システムでビルドすると、すべてのプロジェクトの MSBuild ビルド イベントが同時に生成されます。 大量のイベント データが同時に、または誤った順序で logger に送られてくる可能性があります。 これにより、logger が過負荷となり、ビルド時間の増加や不正確な logger 出力をもたらすだけでなく、ビルドが破損することもあります。 これらの問題を解決するために、MSBuild の logger は順序が誤っているイベントを処理し、イベントとそのソースを関連付けます。  
  
 カスタム転送 logger を作成すると、ログの効率をさらに高めることができます。 カスタム転送 logger はフィルターの役割を果たし、ビルドを開始する前に監視の対象とするイベントを選択できます。 カスタム転送 logger を使用すると、不要なイベントが除外されるため、logger の過負荷、ログの煩雑化、ビルド時間の増加を防ぐことができます。  
  
### <a name="central-logging-model"></a>中央ログ モデル  
 マルチプロセッサ ビルドの場合、MSBuild では "中央ログ モデル" が使用されます。 中央ログ モデルでは、MSBuild.exe のインスタンスがプライマリ ビルド プロセスの役割を果たします。これを "中央ノード" といいます。 中央ノードには、MSBuild.exe のセカンダリ インスタンスがアタッチされます。これを "セカンダリ ノード" といいます。 中央ノードにアタッチされる ILogger ベースの logger を "中央 logger" と呼び、セカンダリ ノードにアタッチされる logger を "セカンダリ logger" と呼びます。  
  
 ビルドを開始すると、セカンダリ logger がイベント トラフィックを中央 logger にルーティングします。 イベントは複数のセカンダリ ノードで発生するため、イベント データは同時に中央ノードに到着しますが、インタリーブされます。 イベントとプロジェクト間の参照やイベントとターゲット間の参照を解決するために、イベント引数には追加のビルド イベント コンテキスト情報が含まれています。  
  
 中央 logger による実装が必要なのは <xref:Microsoft.Build.Framework.ILogger> だけですが、中央 logger をビルドに参加するノードの数で初期化する場合は、<xref:Microsoft.Build.Framework.INodeLogger> も実装することをお勧めします。 エンジンが logger を初期化するときには、次のような <xref:Microsoft.Build.Framework.ILogger.Initialize%2A> メソッドのオーバーロードが呼び出されます。  
  
```  
public interface INodeLogger: ILogger  
{  
    public void Initialize(IEventSource eventSource, int nodeCount);  
}  
```  
  
### <a name="distributed-logging-model"></a>分散ログ モデル  
 中央ログ モデルでは、一度に多数のプロジェクトをビルドする場合など、大量の受信メッセージ トラフィックの発生により、中央ノードが過負荷となることがあり、それがシステムの負担を増大させ、ビルド パフォーマンスの低下につながります。  
  
 この問題を軽減するために、MSBuild は転送 logger の作成によって中央ログ モデルを拡張する "分散ログ モデル" にも対応しています。 転送 logger はセカンダリ ノードにアタッチされ、このノードで生成されるビルド イベントを受け取ります。 転送 logger が通常の logger と異なる点は、イベントをフィルター処理して必要なイベントだけを中央ノードに転送できることです。 これにより、中央ノードへのメッセージ トラフィックが減少するため、パフォーマンスが向上します。  
  
 転送 logger を作成するには、<xref:Microsoft.Build.Framework.IForwardingLogger> の派生インターフェイスである <xref:Microsoft.Build.Framework.ILogger> を実装します。 このインターフェイスは次のように定義されます。  
  
```  
public interface IForwardingLogger: INodeLogger  
{  
    public IEventRedirector EventRedirector { get; set; }  
    public int NodeId { get; set; }  
}  
```  
  
 転送 logger 内のイベントを転送するには、<xref:Microsoft.Build.Framework.IEventRedirector.ForwardEvent%2A> インターフェイスの <xref:Microsoft.Build.Framework.IEventRedirector> メソッドを呼び出します。 パラメーターとして、適切な <xref:Microsoft.Build.Framework.BuildEventArgs> または派生クラスを渡します。  
  
 詳細については、「[転送 logger の作成](../msbuild/creating-forwarding-loggers.md)」を参照してください。  
  
### <a name="attaching-a-distributed-logger"></a>分散 logger のアタッチ  
 コマンド ラインでのビルドで分散 logger をアタッチするには、`/distributedlogger` (短縮形は `/dl`) スイッチを使用します。 logger の型名およびクラス名の形式は、`/logger` スイッチの場合と同じです。ただし、分散 logger は転送 logger と中央 logger という 2 つのログ記録クラスから成ります。 分散 logger をアタッチするコードの例を次に示します。  
  
```  
msbuild.exe *.proj /distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,  
Culture=neutral*XMLForwardingLogger,MyLogger,Version=1.0.2,  
Culture=neutral  
```  
  
 `/dl` スイッチでは、2 つの logger 名をアスタリスク (*) で区切っています。  
  
## <a name="see-also"></a>関連項目
 [ビルド ロガー](../msbuild/build-loggers.md)   
 [転送ロガーの作成](../msbuild/creating-forwarding-loggers.md)
