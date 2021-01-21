---
title: ビルド ロガー | Microsoft Docs
description: MSBuild ロガーを使用してビルドの出力を管理およびカスタマイズし、特定のビルド イベントへの応答としてメッセージ、エラー、または警告を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing loggers
- MSBuild, logging
- logging [MSBuild]
ms.assetid: fa34810d-185a-4d22-92bd-9852915e5f1d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c56de103fa116cbf77ec16dc0116a2897e6ccdce
ms.sourcegitcommit: d3bca34f82de03fa34ecdd72233676c17fb3cb14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92353201"
---
# <a name="build-loggers"></a>ビルド ロガー

ロガーを使うと、ビルドの出力をカスタマイズして、特定のビルド イベントに対する応答のメッセージ、エラー、または警告を表示できます。 各ロガーは、 *Microsoft.Build.Framework.dll* アセンブリで定義されている <xref:Microsoft.Build.Framework.ILogger> インターフェイスを実装する .NET クラスとして実装されます。

ロガーを実装するには 2 つの方法があります。

- <xref:Microsoft.Build.Framework.ILogger> インターフェイスを直接実装します。
- *Microsoft.Build.Utilities.dll* アセンブリで定義されているヘルパー クラス <xref:Microsoft.Build.Utilities.Logger> からクラスを継承します。 <xref:Microsoft.Build.Utilities.Logger> は <xref:Microsoft.Build.Framework.ILogger> を実装し、一部の <xref:Microsoft.Build.Framework.ILogger> メンバーの既定の実装を提供します。

  このトピックでは、<xref:Microsoft.Build.Utilities.Logger> を継承し、特定のビルド イベントに対する応答のメッセージをコンソールに表示する簡単なロガーを作成する方法を説明します。

## <a name="register-for-events"></a>イベントを登録する

ロガーの目的は、ビルド エンジンによって報告されたビルドの進行状況に関する情報を収集し、役に立つ方法でその情報を報告することです。 すべてのロガーは、イベントを登録する <xref:Microsoft.Build.Utilities.Logger.Initialize%2A> メソッドをオーバーライドする必要があります。 この例では、ロガーは <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> イベントを登録しています。

[!code-csharp[msbuild_SimpleConsoleLogger#2](../msbuild/codesnippet/CSharp/build-loggers_1.cs)]

## <a name="respond-to-events"></a>イベントに応答する

特定のイベントを登録したロガーは、発生したイベントを処理する必要があります。 <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> と <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> イベントの場合、ロガーは短い語句と、イベントに関連するプロジェクト ファイルの名前を書き込むだけです。 ロガーからのすべてのメッセージは、コンソール ウィンドウに書き込まれます。

[!code-csharp[msbuild_SimpleConsoleLogger#3](../msbuild/codesnippet/CSharp/build-loggers_2.cs)]

## <a name="respond-to-logger-verbosity-values"></a>ロガーの詳細値に応答する

MSBuild.exe の **-verbosity** スイッチに特定の値が含まれる場合にのみ、イベントから情報を記録したいことがあります。 次の例の <xref:Microsoft.Build.Framework.IEventSource.TargetStarted> イベント ハンドラーは、 **-verbosity** スイッチによって設定される <xref:Microsoft.Build.Utilities.Logger.Verbosity%2A> プロパティが <xref:Microsoft.Build.Framework.LoggerVerbosity>`Detailed` に等しい場合にのみ、メッセージを記録します。

[!code-csharp[msbuild_SimpleConsoleLogger#4](../msbuild/codesnippet/CSharp/build-loggers_3.cs)]

## <a name="specify-a-logger"></a>ロガーを指定する

ロガーがアセンブリにコンパイルされた後は、ビルド中にそのロガーを使うように MSBuild に指示する必要があります。 これは、 *MSBuild.exe* で **-logger** スイッチを使って行います。 *MSBuild.exe* で使用可能なスイッチについて詳しくは、「 [コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」をご覧ください。

次のコマンド ラインは、プロジェクト *MyProject.csproj* をビルドし、 *SimpleLogger.dll* で実装されているロガー クラスを使います。 **-nologo** スイッチはバナーと著作権のメッセージを非表示にし、 **-noconsolelogger** スイッチは既定の MSBuild コンソール ロガーを無効にします。

```cmd
MSBuild -nologo -noconsolelogger -logger:SimpleLogger.dll
```

次のコマンド ラインは同じロガーでプロジェクトをビルドしますが、`Verbosity` レベルは `Detailed` です。

```cmd
MSBuild -nologo -noconsolelogger -logger:SimpleLogger.dll -verbosity:Detailed
```

## <a name="example-1"></a>例 1

### <a name="description"></a>説明

次の例には、ロガーの完全なコードが含まれます。

### <a name="code"></a>コード

[!code-csharp[msbuild_SimpleConsoleLogger#1](../msbuild/codesnippet/CSharp/build-loggers_4.cs)]

## <a name="example-2"></a>例 2

### <a name="description"></a>説明

次の例では、コンソール ウィンドウに表示するのではなくファイルにログを書き込むロガーを実装する方法を示します。

### <a name="code"></a>コード

[!code-csharp[msbuild_BasicLogger#1](../msbuild/codesnippet/CSharp/build-loggers_5.cs)]

## <a name="see-also"></a>関連項目

- [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
