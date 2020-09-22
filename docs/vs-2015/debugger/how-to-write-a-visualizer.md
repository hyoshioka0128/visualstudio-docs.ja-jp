---
title: '方法: ビジュアライザーを記述する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, visualizers
- visualizers, writing
ms.assetid: 625a0d4f-abcc-43f2-9f8c-31c131a4378e
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce50276e4e83a1a055294c8e2b6e09cd0f93d54d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842246"
---
# <a name="how-to-write-a-visualizer"></a>方法 : ビジュアライザーを記述する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Object> および <xref:System.Array> を除く任意のマネージド クラスのオブジェクトのカスタム ビジュアライザーを記述できます。  
  
> [!NOTE]
> **ストア**アプリでは、標準のテキスト、HTML、XML、および JSON ビジュアライザーのみがサポートされています。 カスタム (ユーザーが作成した) ビジュアライザーはサポートされていません。  
  
 デバッガー ビジュアライザーのアーキテクチャには、次の 2 つの部分があります。  
  
- "*デバッガー側*" - Visual Studio デバッガー内で動作します。 デバッガー側のコードは、ビジュアライザーのユーザー インターフェイスを作成し、表示します。  
  
- "*デバッグ対象側*" - Visual Studio がデバッグしているプロセス (*デバッグ対象*) 内で動作します。  
  
  視覚化するデータ オブジェクト (String オブジェクトなど) は、デバッグ対象プロセスに存在します。 このためデバッグ対象側では、そのデータ オブジェクトをデバッガー側に送る必要があります。これによって、デバッガー側では、作成したユーザー インターフェイスを使ってデータ オブジェクトを表示できるようになります。  
  
  デバッガー側は、インターフェイスを実装する *オブジェクトプロバイダー* から視覚化されるように、このデータオブジェクトを受け取り <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> ます。 デバッグ対象側は、から派生した *オブジェクトソース*を介してデータオブジェクトを送信し <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> ます。 オブジェクト プロバイダーは、オブジェクト ソースにデータを戻すこともできます。このため、データの表示だけでなく編集もできるビジュアライザーを記述できます。 オブジェクト プロバイダーは、式エバリュエーターと通信することでオブジェクト ソースと通信するようにオーバーライドできます。  
  
  デバッグ対象側とデバッガー側は、<xref:System.IO.Stream> を介して相互に通信します。 データ オブジェクトを <xref:System.IO.Stream> にシリアル化し、<xref:System.IO.Stream> をデータ オブジェクトに逆シリアル化するメソッドが用意されています。  
  
  デバッグ対象側のコードは、DebuggerVisualizer 属性 (<xref:System.Diagnostics.DebuggerVisualizerAttribute>) で指定します。  
  
  デバッガー側でビジュアライザー ユーザー インターフェイスを作成するには、<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> を継承するクラスを作成し、<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> メソッドをオーバーライドしてインターフェイスを表示する必要があります。  
  
  <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> を使用すると、Windows フォーム、ダイアログ、およびコントロールをビジュアライザーによって表示できます。  
  
  ジェネリック型のサポートは制限されています。 ジェネリック型がオープン型の場合にのみ、そのジェネリック型のビジュアライザーを記述できます。 この制限は、`DebuggerTypeProxy` 属性を使用する場合の制限と同じです。 詳細については、「 [デバッガー Typeproxy 属性の使用](../debugger/using-debuggertypeproxy-attribute.md)」を参照してください。  
  
  カスタムのビジュアライザーでは、セキュリティについての配慮が必要な場合があります。 「 [ビジュアライザーのセキュリティに関する考慮事項](../debugger/visualizer-security-considerations.md)」を参照してください。  
  
  以下の手順は、ビジュアライザーの作成に必要な作業の概要を示したものです。 詳細については、「 [チュートリアル: C# でビジュアライザーを記述](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)する」を参照してください。  
  
### <a name="to-create-the-debugger-side"></a>デバッガー側を作成するには  
  
1. <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> メソッドを使用して、視覚化するオブジェクトをデバッガー側で取得します。  
  
2. <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> を継承するクラスを作成します。  
  
3. <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> メソッドをオーバーライドしてインターフェイスを表示します。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> メソッドを使用して、Windows フォーム、ダイアログ、およびコントロールをインターフェイスの一部として表示します。  
  
4. <xref:System.Diagnostics.DebuggerVisualizerAttribute> をビジュアライザー (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>) に適用します。  
  
### <a name="to-create-the-debuggee-side"></a>デバッグ対象側を作成するには  
  
1. <xref:System.Diagnostics.DebuggerVisualizerAttribute> をビジュアライザー (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>) とオブジェクト ソース (<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>) に適用します。 オブジェクト ソースを省略すると、既定のオブジェクト ソースが使用されます。  
  
2. ビジュアライザーでデータ オブジェクトを表示するだけでなく、編集できるようにする場合は、`TransferData` の `CreateReplacementObject` メソッドまたは <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> メソッドをオーバーライドする必要があります。  
  
## <a name="see-also"></a>参照  
 [カスタムビジュアライザーの作成](../debugger/create-custom-visualizers-of-data.md)   
 [方法: ビジュアライザーをインストールする](../debugger/how-to-install-a-visualizer.md)   
 [方法: ビジュアライザーをテストおよびデバッグする](../debugger/how-to-test-and-debug-a-visualizer.md)   
 [ビジュアライザーのセキュリティに関する考慮事項](../debugger/visualizer-security-considerations.md)
