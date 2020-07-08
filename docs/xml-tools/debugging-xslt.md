---
title: XSLT コードをデバッグする方法
ms.date: 03/05/2019
ms.topic: overview
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: d8e3885aa895cec5ed080b7a8b4d22522d2e9edf
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815618"
---
# <a name="debugging-xslt"></a>XSLT のデバッグ

Visual Studio で XSLT コードをデバッグすることができます。 XSLT デバッガーでは、ブレークポイントの設定や、XSLT 実行状態の表示などがサポートされます。 XSLT デバッガーを使用すると、XSLT スタイル シートや XSLT アプリケーションをデバッグすることができます。

コードのステップ イン、ステップ オーバー、またはステップ アウトを行って、コードを一度に 1 行ずつ実行できます。 XSLT デバッガーのコードのステップ実行機能を使用するためのコマンドは、他の Visual Studio デバッガーの場合と同じです。

デバッグを開始すると、XSLT デバッガーのウィンドウが開き、入力ドキュメントと XSLT 出力が表示されます。

> [!NOTE]
> XSLT デバッガーは、Visual Studio の Professional および Enterprise エディションでのみ使用できます。

## <a name="debug-from-the-xml-editor"></a>XML エディターからデバッグする

エディター内でスタイル シートまたは入力 XML ファイルを開いている場合は、デバッガーを起動できます。 これにより、スタイル シートの設計中にデバッグすることができます。

1. Visual Studio でスタイル シートまたは XML ファイルを開きます。

1. **[XML]** メニューから **[XSLT デバッグを開始]** を選択するか、または **Alt**+**F5** キーを押します。

## <a name="debug-from-an-app-that-uses-xslt"></a>XSLT を使用するアプリからデバッグする

アプリケーションのデバッグ中に XSLT にステップ インすることができます。 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> 呼び出しで **F11** キーを押すと、デバッガーは XSLT コードにステップ インできます。

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> クラスから XSLT へのステップ インは、サポートされていません。 デバッグ中の XSLT へのステップ インをサポートしている XSLT プロセッサは、<xref:System.Xml.Xsl.XslCompiledTransform> クラスだけです。

### <a name="to-start-debugging-an-xslt-application"></a>XSLT アプリケーションのデバッグを開始するには

1. <xref:System.Xml.Xsl.XslCompiledTransform> オブジェクトをインスタンス化するときに、コード内で `enableDebug` パラメーターを `true` に設定します。 この設定によって、コードがコンパイルされるときにデバッグ情報を作成するように XSLT プロセッサに指示します。

1. **F11** キーを押して、XSLT コードにステップ インします。

   XSLT スタイル シートが新しいドキュメントのウィンドウに読み込まれ、XSLT デバッガーが起動されます。

   または、ブレーク ポイントをスタイル シートに追加し、アプリケーションを実行することもできます。

### <a name="example"></a>例

C# XSLT プログラムの例を次に示します。 この例は、XSLT のデバッグを有効にする方法を示しています。

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Xsl;

namespace ConsoleApplication
{
  class Program
  {
    private const string sourceFile = @"c:\data\xsl_files\books.xml";
    private const string stylesheet = @"c:\data\xsl_files\below-average.xsl";
    private const string outputFile = @"c:\data\xsl_files\output.xml";

    static void Main(string[] args)
    {
      // Enable XSLT debugging.
      XslCompiledTransform xslt = new XslCompiledTransform(true);

      // Compile the style sheet.
      xslt.Load(stylesheet);

      // Execute the XSLT transform.
      FileStream outputStream = new FileStream(outputFile, FileMode.Append);
      xslt.Transform(sourceFile, null, outputStream);
    }
  }
}
```

## <a name="xslt-profiler"></a>XSLT プロファイラー

[XSLT プロファイラー](../xml-tools/xslt-profiler.md)は、詳細な XSLT パフォーマンス レポートを作成することにより、開発者が XSLT コード内のパフォーマンス関連の問題を計測、評価、および特定できるようにするツールです。 詳しくは、[XSLT プロファイラー](../xml-tools/xslt-profiler.md)に関する記事をご覧ください。

## <a name="see-also"></a>関連項目

- [チュートリアル: XSLT スタイル シートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
- [最初に Visual Studio デバッガーを見る](../debugger/debugger-feature-tour.md)
- [デバッグの基礎: ブレークポイント](../debugger/using-breakpoints.md)
