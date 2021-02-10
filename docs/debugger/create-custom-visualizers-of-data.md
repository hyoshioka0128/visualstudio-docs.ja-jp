---
title: カスタム データ ビジュアライザーを作成する | Microsoft Docs
description: Visual Studio デバッガー ビジュアライザーはデータを表示するコンポーネントです。 6 つの標準ビジュアライザーと、それ以外を記述したり、ダウンロードしたりする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/27/2020
ms.topic: conceptual
f1_keywords:
- vs.debug.visualizer.troubleshoot
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers
ms.assetid: c24c006f-f2ac-429f-89db-677fc0c6e1ea
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7f3d9a907d0857e918069fc4542d59d87242d609
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99865840"
---
# <a name="create-custom-data-visualizers"></a>カスタム データ ビジュアライザーを作成する

 "*ビジュアライザー*" は、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] デバッガーのユーザー インターフェイスの一部で、データ型に適した方法で変数またはオブジェクトが表示されます。 たとえば、HTML ビジュアライザーでは、HTML 文字列が解釈され、結果がブラウザー ウィンドウに表示されるとおりに表示されます。 また、ビットマップ ビジュアライザーは、ビットマップ構造が解釈され、それが表すグラフィックが表示されます。 一部のビジュアライザーでは、データを表示するだけでなく、変更することもできます。

 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] デバッガーには、6 つの標準的なビジュアライザーが用意されています。 テキスト、HTML、XML、JSON ビジュアライザーは、文字列のオブジェクトに対して機能します。 WPF ツリー ビジュアライザーでは、WPF オブジェクトのビジュアル ツリーのプロパティが表示されます。 データセット ビジュアライザーは、DataSet オブジェクト、DataView オブジェクト、DataTable オブジェクトに対して機能します。

他にも、Microsoft、サード パーティ、コミュニティからダウンロードできるビジュアライザーがあります。 また、独自のビジュアライザーを作成して、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] デバッガーにインストールすることもできます。

デバッガーでは、ビジュアライザーは拡大鏡アイコン ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン") で表されます。 このアイコンを **[データヒント]** 、デバッガーの **[ウォッチ]** ウィンドウ、または **[クイックウォッチ]** ダイアログ ボックスで選択し、対応するオブジェクトに適したビジュアライザーを選択することができます。

## <a name="write-custom-visualizers"></a>カスタム ビジュアライザーを作成する

 > [!NOTE]
 > ネイティブ コードのカスタム ビジュアライザーを作成するには、[SQLite ネイティブ デバッガー ビジュアライザー](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/SqliteVisualizer)のサンプルを参照してください。 カスタム ビジュアライザーは、UWP および Windows 8.x アプリではサポートされていません。

<xref:System.Object> および <xref:System.Array> を除く任意のマネージド クラスのオブジェクトのカスタム ビジュアライザーを記述できます。

デバッガー ビジュアライザーのアーキテクチャには、次の 2 つの部分があります。

- "*デバッガー側*" - Visual Studio デバッガー内で動作し、ビジュアライザーのユーザー インターフェイスが作成され表示されます。

- "*デバッグ対象側*" - Visual Studio がデバッグしているプロセス (*デバッグ対象*) 内で動作します。 視覚化するデータ オブジェクト (たとえば、文字列のオブジェクト) は、デバッグ対象プロセス内に存在します。 デバッグ対象側は、オブジェクトがデバッガー側に送信され、デバッガー側では、それが作成されたユーザー インターフェイスに表示されます。

デバッガー側では、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> インターフェイスを実装する "*オブジェクト プロバイダー*" からデータ オブジェクトが受け取ります。 デバッグ対象側では、<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> から派生する "*オブジェクト ソース*" を介してオブジェクトが送られます。

オブジェクト プロバイダーは、オブジェクト ソースにデータを送り返すこともできます。これにより、データを編集できるビジュアライザーを作成できます。 式エバリュエーターおよびオブジェクト ソースと対話するには、オブジェクト プロバイダーをオーバーライドします。

デバッガー対象側とデバッガー側は、<xref:System.IO.Stream> メソッドを介して相互に通信します。このメソッドは、データ オブジェクトを <xref:System.IO.Stream> にシリアル化して、<xref:System.IO.Stream> をデータ オブジェクトに逆シリアル化します。

型がオープン型の場合のみ、ジェネリック型のビジュアライザーを作成できます。 この制限は、`DebuggerTypeProxy` 属性を使用する場合の制限と同じです。 詳細については、[DebuggerTypeProxy 属性の使用](../debugger/using-debuggertypeproxy-attribute.md)に関するページを参照してください。

カスタムのビジュアライザーでは、セキュリティについての配慮が必要な場合があります。 「[ビジュアライザーのセキュリティに関する考慮事項](../debugger/visualizer-security-considerations.md)」を参照してください。

以下の手順では、ビジュアライザーの作成について概要を説明します。 詳細な手順については、「[チュートリアル: C# でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)」または「[チュートリアル: Visual Basic でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)」を参照してください。

### <a name="to-create-the-debugger-side"></a>デバッガー側を作成するには

デバッガー側でビジュアライザー ユーザー インターフェイスを作成するには、<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> を継承するクラスを作成し、<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> メソッドをオーバーライドしてインターフェイスを表示する必要があります。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> を使用すると、ビジュアライザーで Windows フォーム、ダイアログ、コントロールを表示できます。

1. <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> メソッドを使用して、視覚化するオブジェクトをデバッガー側で取得します。

1. <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> を継承するクラスを作成します。

1. <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> メソッドをオーバーライドしてインターフェイスを表示します。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> メソッドを使用して、インターフェイスで Windows フォーム、ダイアログ、コントロールを表示します。

4. <xref:System.Diagnostics.DebuggerVisualizerAttribute> を適用して、表示するビジュアライザーを指定します (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>)。

### <a name="to-create-the-visualizer-object-source-for-the-debuggee-side"></a>デバッグ対象側のビジュアライザー オブジェクト ソースを作成するには

デバッガー側のコードで <xref:System.Diagnostics.DebuggerVisualizerAttribute> を編集して、視覚化する型 (デバッグ対象側のオブジェクト ソース) (<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>) を指定します。 `Target` プロパティにオブジェクト ソースが設定されます。 オブジェクト ソースを省略すると、ビジュアライザーは既定のオブジェクト ソースを使用します。

::: moniker range=">=vs-2019"
デバッグ対象側のコードには、視覚化されたオブジェクト ソースが含まれています。 データ オブジェクトでは、<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> のメソッドをオーバーライドできます。 スタンドアロン ビジュアライザーを作成する場合は、デバッグ対象側の DLL が必要です。
::: moniker-end

デバッグ対象側のコードで:

- ビジュアライザーでデータ オブジェクトを編集できるようにするには、オブジェクト ソースを <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> から継承し、`TransferData` または `CreateReplacementObject` メソッドをオーバーライドする必要があります。

- ビジュアライザー内でマルチターゲットをサポートする必要がある場合は、デバッグ対象側のプロジェクト ファイル内で次のターゲット フレームワーク モニカー (TFM) を使用できます。

   ```xml
   <TargetFrameworks>net20;netstandard2.0;netcoreapp2.0</TargetFrameworks>
   ```

   これらはサポートされている唯一の TFM です。

## <a name="see-also"></a>関連項目

- [チュートリアル: C# でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [チュートリアル: Visual Basic でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [方法: ビジュアライザーをインストールする](../debugger/how-to-install-a-visualizer.md)
- [方法: ビジュアライザーをテストおよびデバッグする](../debugger/how-to-test-and-debug-a-visualizer.md)
- [ビジュアライザー API リファレンス](../debugger/visualizer-api-reference.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)