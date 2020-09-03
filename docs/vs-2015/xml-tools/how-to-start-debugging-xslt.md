---
title: '方法: XSLT のデバッグを開始する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 8358335a-fcb0-45e0-a37e-45b43e49ec0a
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 09471b9e62b758e4e02e054494ed108532bbd301
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656328"
---
# <a name="how-to-start-debugging-xslt"></a>方法 : XSLT のデバッグを開始する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XSLT デバッガーを使用すると、XSLT スタイル シートや XSLT アプリケーションをデバッグすることができます。 デバッグの際には、コードのステップ イン、ステップ オーバー、またはステップ アウトを行って、コードを一度に 1 行ずつ実行できます。 コードのステップ実行機能を使用するためのコマンドは、XSLT デバッガーを使用する場合と、他の Visual Studio デバッガーを使用する場合とで変わりません。 デバッグを開始すると、XSLT デバッガーのウィンドウが開き、入力ドキュメントと XSLT 出力が表示されます。

## <a name="xml-editor"></a>XML エディター
 デバッガーは、XML エディターから起動できます。 このため、スタイル シートの設計中にデバッグすることができます。

#### <a name="to-start-debugging-from-a-style-sheet"></a>スタイル シートからデバッグを開始するには

1. XML エディターでスタイル シートを開きます。

2. [ **XML** ] メニューの [ **XSL のデバッグ**] を選択します。

#### <a name="to-start-debugging-from-an-xml-input-document"></a>XML 入力ドキュメントからデバッグを開始するには

1. XML エディターで XML ドキュメントを開きます。

2. [ **XML** ] メニューの [ **XSL のデバッグ**] を選択します。

## <a name="xslt-from-other-languages"></a>他の言語の XSLT
 アプリケーションのデバッグ中に XSLT にステップ インすることもできます。  呼び出しで F11 キーを押すと、デバッガーは XSLT コードにステップ インできます。

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> クラスから XSLT へのステップ インは、サポートされていません。 デバッグ中の XSLT へのステップ インをサポートしている XSLT プロセッサは、<xref:System.Xml.Xsl.XslCompiledTransform> クラスだけです。

#### <a name="to-start-debugging-an-xslt-application"></a>XSLT アプリケーションのデバッグを開始するには

1. <xref:System.Xml.Xsl.XslCompiledTransform> オブジェクトをインスタンス化するときに、コード内で `enableDebug` パラメーターを `true` に設定します。

     この設定によって、コードがコンパイルされるときにデバッグ情報を作成するように XSLT プロセッサに指示します。

2. F11 キーを押して、XSLT コードにステップ インします。

     XSLT スタイル シートが新しいドキュメントのウィンドウに読み込まれ、XSLT デバッガーが起動されます。

     または、ブレーク ポイントをスタイル シートに追加し、アプリケーションを実行することもできます。

### <a name="example"></a>例
 C# XSLT プログラムの例を次に示します。 この例は、XSLT のデバッグを有効にする方法を示しています。

```
using System;
using System.IO;
using System.Xml;
using System.Xml.Xsl;

namespace ConsoleApplication
{
  class Program
  {
    private const string sourceFile = @"c:\data\xsl_files\books.xml";
    private const string stylesheet = @"c:\data\xsl_files\belowAvg.xsl";
    private const string outputFile = @"c:\data\xsl_files\output.xml";

    static void Main(string[] args)
    {
      // Enable XSLT debugging.
      XslCompiledTransform xslt = new XslCompiledTransform(true);

      // Compile the style sheet.
      xslt.Load(stylesheet)

      // Execute the XSLT transform.
      FileStream outputStream = new FileStream(outputFile, FileMode.Append);
      xslt.Transform(sourceFile, null, outputStream);
    }
  }
}
```

## <a name="see-also"></a>参照
 [チュートリアル: XSLT スタイルシートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)[コードのステップ](https://msdn.microsoft.com/8791dac9-64d1-4bb9-b59e-8d59af1833f9)実行の概要
