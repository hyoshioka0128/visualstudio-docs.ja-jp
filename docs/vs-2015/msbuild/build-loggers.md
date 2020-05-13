---
title: ビルド ロガー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing loggers
- MSBuild, logging
- logging [MSBuild]
ms.assetid: fa34810d-185a-4d22-92bd-9852915e5f1d
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2908c8217070196de1b2d3cd4f1c5f8d8f2868a5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160434"
---
# <a name="build-loggers"></a>ビルド ロガー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ロガーを使うと、ビルドの出力をカスタマイズして、特定のビルド イベントに対する応答のメッセージ、エラー、または警告を表示できます。 各ロガーは、Microsoft.Build.Framework.dll アセンブリで定義されている <xref:Microsoft.Build.Framework.ILogger> インターフェイスを実装する .NET クラスとして実装されます。  
  
 ロガーを実装するには 2 つの方法があります。  
  
- <xref:Microsoft.Build.Framework.ILogger> インターフェイスを直接実装します。  
  
- Microsoft.Build.Utilities.dll アセンブリで定義されているヘルパー クラス <xref:Microsoft.Build.Utilities.Logger> からクラスを継承します。 <xref:Microsoft.Build.Utilities.Logger> は <xref:Microsoft.Build.Framework.ILogger> を実装し、一部の <xref:Microsoft.Build.Framework.ILogger> メンバーの既定の実装を提供します。  
  
  このトピックでは、<xref:Microsoft.Build.Utilities.Logger> を継承し、特定のビルド イベントに対する応答のメッセージをコンソールに表示する簡単なロガーを作成する方法を説明します。  
  
## <a name="registering-for-events"></a>イベントの登録  
 ロガーの目的は、ビルド エンジンによって報告されたビルドの進行状況に関する情報を収集し、役に立つ方法でその情報を報告することです。 すべてのロガーは、イベントを登録する <xref:Microsoft.Build.Utilities.Logger.Initialize%2A> メソッドをオーバーライドする必要があります。 この例では、ロガーは <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> イベントを登録しています。  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#2](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#2)]  
  
## <a name="responding-to-events"></a>イベントへの応答  
 特定のイベントを登録したロガーは、発生したイベントを処理する必要があります。 <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> と <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> イベントの場合、ロガーは短い語句と、イベントに関連するプロジェクト ファイルの名前を書き込むだけです。 ロガーからのすべてのメッセージは、コンソール ウィンドウに書き込まれます。  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#3](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#3)]  
  
## <a name="responding-to-logger-verbosity-values"></a>ロガーの詳細値への応答  
 MSBuild.exe の **/verbosity** スイッチに特定の値が含まれる場合にのみ、イベントから情報を記録したいことがあります。 次の例の <xref:Microsoft.Build.Framework.IEventSource.TargetStarted> イベント ハンドラーは、 **/verbosity** スイッチによって設定される <xref:Microsoft.Build.Utilities.Logger.Verbosity%2A> プロパティが <xref:Microsoft.Build.Framework.LoggerVerbosity>`Detailed` に等しい場合にのみ、メッセージを記録します。  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#4](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#4)]  
  
## <a name="specifying-a-logger"></a>ロガーの指定  
 ロガーがアセンブリにコンパイルされた後は、ビルドの間にそのロガーを使うように [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に指定する必要があります。 これは、MSBuild.exe で **/logger** スイッチを使って行います。 MSBuild.exe で使用可能なスイッチについて詳しくは、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」をご覧ください。  
  
 次のコマンド ラインは、プロジェクト `MyProject.csproj` をビルドし、`SimpleLogger.dll` で実装されているロガー クラスを使います。 **/nologo** スイッチはバナーと著作権のメッセージを非表示にし、 **/noconsolelogger** スイッチは既定の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] コンソール ロガーを無効にします。  
  
```  
MSBuild /nologo /noconsolelogger /logger:SimpleLogger.dll  
```  
  
 次のコマンド ラインは同じロガーでプロジェクトをビルドしますが、`Verbosity` レベルは `Detailed` です。  
  
```  
MSBuild /nologo /noconsolelogger /logger:SimpleLogger.dll /verbosity:Detailed  
```  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例には、ロガーの完全なコードが含まれます。  
  
### <a name="code"></a>コード  
 [!code-csharp[msbuild_SimpleConsoleLogger#1](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#1)]  
  
### <a name="comments"></a>コメント  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、コンソール ウィンドウに表示するのではなくファイルにログを書き込むロガーを実装する方法を示します。  
  
### <a name="code"></a>コード  
 [!code-csharp[msbuild_BasicLogger#1](../snippets/csharp/VS_Snippets_Misc/msbuild_BasicLogger/CS/msbuild_BasicLogger.cs#1)]  
  
### <a name="comments"></a>コメント  
  
## <a name="see-also"></a>関連項目
 [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)
