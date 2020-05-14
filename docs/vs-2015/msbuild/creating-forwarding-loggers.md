---
title: 転送 logger の作成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, forwarding loggers
- MSBuild, logging
ms.assetid: 3aebf9c8-b62c-4cb2-b2d6-8cdfcd369a24
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ecc9bae7176c0d8c0f79452baff87a7a697db459
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184027"
---
# <a name="creating-forwarding-loggers"></a>転送 logger の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

転送 logger では、マルチプロセッサ システムでプロジェクトをビルドするときに監視の対象とするイベントを選択できるため、ログの効率を高めることができます。 転送 logger を有効にすることで、不要なイベントによる中心 logger の過負荷、ビルドの低速化、およびログの煩雑化を回避できます。  
  
 転送 logger を作成する場合は、<xref:Microsoft.Build.Framework.IForwardingLogger> インターフェイスを実装してそのメソッドを手動で実装するか、<xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> クラスとその定義済みメソッドを使用できます (ほとんどのアプリケーションでは、後者で十分です)。  
  
## <a name="register-events-and-respond-to-them"></a>イベントの登録とイベントへの応答  
 転送 logger は、セカンダリ ビルド エンジン (マルチプロセッサ システムでのビルド時にメイン ビルド プロセスによって作成されるワーカー プロセス) から報告されるビルド イベントの情報を収集します。 次に、転送 logger は指定された手順に基づいて、中心 logger に転送するイベントを選択します。  
  
 監視対象のイベントを処理するには、転送 logger を登録する必要があります。 イベントのために登録するには、logger で <xref:Microsoft.Build.Utilities.Logger.Initialize%2A> メソッドをオーバーライドする必要があります。 このメソッドには省略可能なパラメーターである `nodecount` が追加されました。このパラメーターをシステムのプロセッサ数に設定できます (既定値は 1 です)。  
  
 監視できるイベントの例として、<xref:Microsoft.Build.Framework.IEventSource.TargetStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectStarted>、および <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> などがあります。  
  
 マルチプロセッサ環境では、イベント メッセージが誤った順序で受信される可能性があります。 したがって、転送 logger でイベント ハンドラーを使用してイベントを評価し、どのイベントをリダイレクターに渡して中心 logger に転送するかを判断するためにプログラミングする必要があります。 これを行うために、各メッセージにアタッチされた <xref:Microsoft.Build.Framework.BuildEventContext> クラスを使用します。このクラスによって、転送が必要なイベントを特定し、イベントの名前を <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> クラス (またはそのサブクラス) に渡すことができます。 このメソッドを使用した場合は、それ以外にイベントを転送するためのコーディングを行う必要はありません。  
  
## <a name="specify-a-forwarding-logger"></a>転送 logger の指定  
 転送 logger がアセンブリにコンパイルされたら、ビルド時に使用することを [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に通知する必要があります。 そのためには、MSBuild.exe と共に `/FileLogger`、`/FileLoggerParameters`、および `/DistributedFileLogger` スイッチを使用します。 `/FileLogger` スイッチは、logger が直接アタッチされていることを MSBuild.exe に通知します。 `/DistributedFileLogger` スイッチは、ノードごとにログ ファイルが存在することを意味します。 転送 logger にパラメーターを設定するには、`/FileLoggerParameters` スイッチを使用します。 上記およびその他の MSBuild.exe スイッチの詳細については、[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)に関するページを参照してください。  
  
## <a name="multi-processor-aware-loggers"></a>マルチプロセッサ対応の logger  
 マルチプロセッサ システムでプロジェクトをビルドする場合、各プロセッサからのビルド メッセージが自動的に一貫した順序でインタリーブされるわけではありません。 したがって、各メッセージにアタッチされる <xref:Microsoft.Build.Framework.BuildEventContext> クラスを使用して、メッセージ グループ化の優先順位を確立する必要があります。 マルチプロセッサ ビルドの詳細については、「[マルチプロセッサ環境でのログ](../msbuild/logging-in-a-multi-processor-environment.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目
 [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)   
 [ビルド ロガー](../msbuild/build-loggers.md)   
 [マルチプロセッサ環境でのログ](../msbuild/logging-in-a-multi-processor-environment.md)
