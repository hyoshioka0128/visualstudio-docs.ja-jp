---
title: XSLT コードをデバッグする方法
ms.date: 03/05/2019
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: f6f4a1ce60f04bcea6e21b52db9347a95292dab2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592855"
---
# <a name="debugging-xslt"></a>XSLT のデバッグ

Visual Studio で XSLT コードをデバッグできます。 XSLT デバッガーは、ブレークポイントの設定、XSLT 実行状態の表示などをサポートしています。 Xslt デバッガーを使用すると、xslt スタイルシートや XSLT アプリケーションをデバッグできます。

コードをステップイン、ステップオーバー、またはステップアウトすることで、一度に1行ずつコードを実行できます。 XSLT デバッガーのコードステップ機能を使用するためのコマンドは、他の Visual Studio デバッガーのコマンドと同じです。

デバッグを開始すると、XSLT デバッガーのウィンドウが開き、入力ドキュメントと XSLT 出力が表示されます。

> [!NOTE]
> XSLT デバッガーは、Visual Studio の Professional および Enterprise エディションでのみ使用できます。

## <a name="debug-from-the-xml-editor"></a>XML エディターからのデバッグ

エディターでスタイルシートまたは入力 XML ファイルを開いている場合は、デバッガーを起動できます。 これにより、スタイルシートをデザインするときにデバッグを行うことができます。

1. Visual Studio でスタイルシートまたは XML ファイルを開きます。

1. **[XML]** メニューの **[XSLT デバッグの開始]** を選択するか、 **Alt**キーを押し+**F5**キーを押します。

## <a name="debug-from-an-app-that-uses-xslt"></a>XSLT を使用するアプリからデバッグする

アプリケーションのデバッグ中に XSLT にステップインできます。 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> の呼び出しで**F11**キーを押すと、デバッガーは XSLT コードにステップインできます。

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> クラスから XSLT へのステップ インは、サポートされていません。 デバッグ中の XSLT へのステップ インをサポートしている XSLT プロセッサは、<xref:System.Xml.Xsl.XslCompiledTransform> クラスだけです。

### <a name="to-start-debugging-an-xslt-application"></a>XSLT アプリケーションのデバッグを開始するには

1. <xref:System.Xml.Xsl.XslCompiledTransform> オブジェクトをインスタンス化するときに、コード内で `enableDebug` パラメーターを `true` に設定します。 この設定によって、コードがコンパイルされるときにデバッグ情報を作成するように XSLT プロセッサに指示します。

1. **F11**キーを押して、XSLT コードにステップインします。

   XSLT スタイルシートが新しいドキュメントウィンドウに読み込まれ、XSLT デバッガーが起動します。

   または、ブレーク ポイントをスタイル シートに追加し、アプリケーションを実行することもできます。

### <a name="example"></a>使用例

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

[Xslt プロファイラー](../xml-tools/xslt-profiler.md)は、詳細な xslt パフォーマンスレポートを作成することによって、開発者が xslt コードのパフォーマンス関連の問題を測定、評価、および特定するためのツールです。 詳細については、「 [XSLT profiler](../xml-tools/xslt-profiler.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [チュートリアル: XSLT スタイルシートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
- [最初に Visual Studio デバッガーを確認する](../debugger/debugger-feature-tour.md)
- [デバッグの基礎: ブレークポイント](../debugger/using-breakpoints.md)
