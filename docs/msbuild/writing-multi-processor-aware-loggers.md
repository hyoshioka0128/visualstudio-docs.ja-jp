---
title: マルチプロセッサ対応の logger の記述 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, multi-proc aware loggers
- multi-proc loggers
- loggers, multi-proc
ms.assetid: ff987d1b-1798-4803-9ef6-cc8fcc263516
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 886e012b026ef17b512a7e134d080382744783ef
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77630748"
---
# <a name="write-multi-processor-aware-loggers"></a>マルチプロセッサ対応のロガーの記述

MSBuild では複数のプロセッサを使用できるため、プロジェクトのビルド時間が短縮されますが、同時にビルド イベント ログの複雑性も高まります。 シングルプロセッサ環境では、イベント、メッセージ、警告、およびエラーが順序に従った予測可能な方法で logger に到着します。 それに対し、マルチプロセッサ環境では、イベントが複数のソースから同時に、または誤った順序で送られてくることがあります。 この問題を解決するために、MSBuild にはマルチプロセッサ対応のロガーと新しいログ モデルが導入されており、カスタム "転送ロガー" を作成できます。

## <a name="multi-processor-logging-challenges"></a>マルチプロセッサ ログの問題点

 1 つ以上のプロジェクトをマルチプロセッサまたはマルチコアのシステム上でビルドすると、すべてのプロジェクトの MSBuild ビルド イベントが同時に生成されます。 大量のイベント メッセージが同時に、または誤った順序で logger に送られてくる可能性があります。 MSBuild 2.0 のロガーはこのような状況に対応するように設計されていないため、ロガーが過負荷となり、ビルド時間の増加や不正確なロガー出力をもたらすだけでなく、ビルドが破損することもあります。 これらの問題を解決するために、MSBuild 3.5 以降のロガーでは順序が誤っているイベントを処理し、イベントとそのソースを関連付けることができます。

 カスタム転送 logger を作成すると、ログの効率をさらに高めることができます。 カスタム転送 logger はフィルターの役割を果たし、ビルドを開始する前に監視の対象とするイベントのみを選択できます。 カスタム転送 logger を使用すると、不要なイベントが除外されるため、logger の過負荷、ログの煩雑化、ビルド時間の増加を防ぐことができます。

## <a name="multi-processor-logging-models"></a>マルチプロセッサ ログ モデル

 マルチプロセッサに関連するビルド上の問題を解決するために、MSBuild では中央ログ モデルと分散ログ モデルという 2 つのログ モデルがサポートされています。

### <a name="central-logging-model"></a>中央ログ モデル

 中央ログ モデルでは、*MSBuild.exe* の 1 つのインスタンスが "中央ノード" となり、中央ノードの子インスタンス ("セカンダリ ノード") が中央ノードにアタッチされ、それによってビルド タスクの実行が可能になります。

 ![中央ロガー モデル](../msbuild/media/centralnode.png "CentralNode")

 中央ノードにアタッチされる各種の logger を "中央 logger" といいます。 いずれの logger でも一度に 1 つのインスタンスのみ中央ノードにアタッチできます。

 ビルドを開始すると、セカンダリ ノードがビルド イベントを中央ノードにルーティングします。 中央ノードは、受け取ったすべてのイベントとセカンダリ ノードのイベントを 1 つ以上のアタッチされた中央 logger にルーティングします。 それらの logger は、受け取ったデータに基づくログ ファイルを作成します。

 中央 logger による実装が必要なのは <xref:Microsoft.Build.Framework.ILogger> だけですが、中央 logger がビルドに参加するノードの数で初期化されるように、<xref:Microsoft.Build.Framework.INodeLogger> も実装することをお勧めします。 エンジンが logger を初期化するときには、次のような <xref:Microsoft.Build.Framework.ILogger.Initialize%2A> メソッドのオーバーロードが呼び出されます。

```csharp
public interface INodeLogger: ILogger
{
    public void Initialize(IEventSource eventSource, int nodeCount);
}
```

 <xref:Microsoft.Build.Framework.ILogger> ベースの既存の logger を中央 logger として利用し、ビルドにアタッチすることができます。 ただし、マルチプロセッサ ログ シナリオと誤った順序のイベントの明示的なサポートが組み込まれていない中央 logger を使用すると、ビルドの破損や無意味な出力の生成につながる可能性があります。

### <a name="distributed-logging-model"></a>分散ログ モデル

 中央ログ モデルでは、一度に多数のプロジェクトをビルドする場合など、大量の受信メッセージ トラフィックが発生し、中央ノードが過負荷となることがあります。 その結果、システム リソースの負荷増大やビルド パフォーマンスの低下を招くことがあります。 この問題を軽減するために、MSBuild では分散ログ モデルがサポートされています。

 ![分散ログ モデル](../msbuild/media/distnode.png "DistNode")

 分散ログ モデルは、転送 logger の作成を可能にすることにより、中央ログ モデルを拡張したものです。

#### <a name="forwarding-loggers"></a>転送ロガー

 転送 logger は、イベント フィルターを備えた補助的で簡易な logger であり、セカンダリ ノードにアタッチされ、そのノードで生成されたビルド イベントを受け取ります。 転送 logger は受け取ったイベントをフィルター処理し、指定されたイベントだけを中央ノードに転送します。 これによって、中央ノードに送信されるメッセージ トラフィックが減少し、全体的なビルド パフォーマンスが向上します。

 分散ログには次の 2 つの使用方法があります。

- <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> という名前の用意された転送 logger をカスタマイズします。

- カスタム転送 logger を独自に作成します。

ConfigurableForwardingLogger を実際の要件に合わせて変更できます。 これを行うには、このロガーをコマンド ラインで *MSBuild.exe* を使用して呼び出し、このロガーから中央ノードに転送するビルド イベントを指定します。

また、カスタム転送 logger を作成することもできます。 カスタム転送 logger を作成すると、logger の動作を細かく調整できます。 ただし、カスタム転送 logger を作成する作業は ConfigurableForwardingLogger をカスタマイズする場合より複雑です。 詳細については、「[転送 logger の作成](../msbuild/creating-forwarding-loggers.md)」を参照してください。

## <a name="using-the-configurableforwardinglogger-for-simple-distributed-logging"></a>ConfigurableForwardingLogger を使用した簡単な分散ログ

 ConfigurableForwardingLogger またはカスタム転送ロガーをアタッチするには、*MSBuild.exe* を使用したコマンド ライン ビルドに `-distributedlogger` スイッチ (短縮形は `-dl`) を指定します。 logger の型名およびクラス名の形式は、`-logger` スイッチの場合と同じです。ただし、分散 logger は常に転送 logger と中央 logger という 2 つのログ記録クラスから成ります。 XMLForwardingLogger というカスタム転送 logger をアタッチするコードの例を次に示します。

```cmd
msbuild.exe myproj.proj -distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,Culture=neutral*XMLForwardingLogger,MyLogger,Version=1.0.2,Culture=neutral
```

> [!NOTE]
> `-dl` スイッチでは、2 つの logger 名をアスタリスク (*) で区切る必要があります。

 ConfigurableForwardingLogger の使用方法は、通常の MSBuild ではなく ConfigurableForwardingLogger ロガーをアタッチし、ConfigurableForwardingLogger から中央ノードに渡すイベントをパラメーターとして指定する点を除き、他のロガーと同じです (「[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)」を参照)。

 たとえば、ビルドの開始および終了の時点とエラーの発生時のみ通知を受け取る場合は、パラメーターとして `BUILDSTARTEDEVENT`、`BUILDFINISHEDEVENT`、および `ERROREVENT` を渡します。 複数のパラメーターを渡す場合は、パラメーターをセミコロンで区切ります。 ConfigurableForwardingLogger を使用して `BUILDSTARTEDEVENT`、`BUILDFINISHEDEVENT`、`ERROREVENT` の各イベントのみを転送する方法を次の例に示します。

```cmd
msbuild.exe myproj.proj -distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,Culture=neutral*ConfigureableForwardingLogger,C:\My.dll;BUILDSTARTEDEVENT; BUILDFINISHEDEVENT;ERROREVENT
```

 ConfigurableForwardingLogger で使用できるパラメーターの一覧を次に示します。

|ConfigurableForwardingLogger のパラメーター|
| - |
|BUILDSTARTEDEVENT|
|BUILDFINISHEDEVENT|
|PROJECTSTARTEDEVENT|
|PROJECTFINISHEDEVENT|
|TARGETSTARTEDEVENT|
|TARGETFINISHEDEVENT|
|TASKSTARTEDEVENT|
|TASKFINISHEDEVENT|
|ERROREVENT|
|WARNINGEVENT|
|HIGHMESSAGEEVENT|
|NORMALMESSAGEEVENT|
|LOWMESSAGEEVENT|
|CUSTOMEVENT|
|COMMANDLINE|
|PERFORMANCESUMMARY|
|NOSUMMARY|
|SHOWCOMMANDLINE|

## <a name="see-also"></a>関連項目

- [転送 logger の作成](../msbuild/creating-forwarding-loggers.md)