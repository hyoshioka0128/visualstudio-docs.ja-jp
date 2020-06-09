---
title: ビジュアライザーのアーキテクチャ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 6aad395f-7170-4d9e-b2b8-a5faf453380e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a6dfbc8c57ff2e78bf0c6ebbd4e9899c372d7084
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187161"
---
# <a name="visualizer-architecture"></a>ビジュアライザーのアーキテクチャ
デバッガー ビジュアライザーのアーキテクチャには、次の 2 つの部分があります。

- "*デバッガー側*" - Visual Studio デバッガー内で動作します。 デバッガー側のコードは、ビジュアライザーのユーザー インターフェイスを作成し、表示します。

- "*デバッグ対象側*" - Visual Studio がデバッグしているプロセス (*デバッグ対象*) 内で動作します。

  ビジュアライザーは、データ オブジェクトの内容を、意味のある理解しやすい形式で表示 ("*視覚化*") できるようにするためのデバッガーのコンポーネントです。 データ オブジェクトの編集をサポートするビジュアライザーもあります。 カスタム ビジュアライザーを作成すれば、独自のデータ型を処理できるようにデバッガーを拡張することも可能です。

  視覚化対象であるデータ オブジェクトは、デバッグ中のプロセス ("*デバッグ対象*" プロセス) 内に存在します。 データを表示するユーザー インターフェイスは、Visual Studio デバッガー プロセス内で作成されます。

|デバッガー プロセス|デバッグ対象プロセス|
|----------------------|----------------------|
|デバッガーのユーザー インターフェイス (データヒント、ウォッチ ウィンドウ、クイック ウォッチ)|視覚化の対象となるデータ オブジェクト|

 デバッガーのインターフェイス内でデータ オブジェクトを視覚化するには、2 つのプロセス間の通信を実現するためのコードを記述する必要があります。 したがって、ビジュアライザーのアーキテクチャは、"*デバッガー側*" コードと "*デバッグ対象側*" コードという、2 つの要素で構成されることになります。

 デバッガー側コードでは、自身のユーザー インターフェイスが作成されます。このインターフェイスは、デバッガーのインターフェイス (データヒント、ウォッチ ウィンドウ、またはクイック ウォッチ) から呼び出すことができます。 ビジュアライザーのインターフェイスは、<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> クラスおよび <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> インターフェイスを使用して作成します。 ビジュアライザーのすべての API に共通することですが、DialogDebuggerVisualizer および IDialogVisualizerService は、<xref:Microsoft.VisualStudio.DebuggerVisualizers> 名前空間に存在します。

|デバッガー側|デバッグ対象側|
|-------------------|-------------------|
|DialogDebuggerVisualizer クラス<br /><br /> IDialogVisualizerService インターフェイス|データ オブジェクト|

 ユーザー インターフェイスは、視覚化の対象となるデータを、デバッガー側に存在するオブジェクト プロバイダーから取得します。

|デバッガー側|デバッグ対象側|
|-------------------|-------------------|
|DialogDebuggerVisualizer クラス<br /><br /> IDialogVisualizerService インターフェイス|データ オブジェクト|
|オブジェクト プロバイダー (<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> を実装)||

 デバッグ対象側には、対応するオブジェクトが存在します。これをオブジェクト ソースと呼びます。

|デバッガー側|デバッグ対象側|
|-------------------|-------------------|
|DialogDebuggerVisualizer クラス<br /><br /> IDialogVisualizerService インターフェイス|データ オブジェクト|
|オブジェクト プロバイダー (<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> を実装)|オブジェクト ソース (<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> から派生)|

 オブジェクト プロバイダーは、視覚化の対象となるオブジェクト データをビジュアライザーの UI に提供します。 オブジェクト プロバイダーは、このオブジェクト データをオブジェクト ソースから取得します。 オブジェクト プロバイダーおよびオブジェクト ソースには、デバッガー側とデバッグ対象側との間でオブジェクト データをやり取りするための API が用意されています。

 ビジュアライザーはすべて、視覚化の対象となるデータ オブジェクトを取得する必要があります。 次の表は、この目的で使用されるオブジェクト プロバイダーの API と、それに対応するオブジェクト ソースの API を示しています。

|オブジェクト プロバイダー|オブジェクト ソース|
|---------------------|-------------------|
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A><br /><br /> または<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A>|

 オブジェクト プロバイダーには、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A> と <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A> の 2 つの API が存在しています。 どちらの API を使用しても、オブジェクト ソースの <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A> が呼び出されます。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A?displayProperty=fullName> を呼び出すと、視覚化の対象となるオブジェクトがシリアル化されて <xref:System.IO.Stream?displayProperty=fullName> に格納されます。

 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A?displayProperty=fullName> では、データがオブジェクト形式へと逆シリアル化されるため、このデータをそのまま <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> で作成した UI に表示できます。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> では、データが未加工の `Stream` として格納されるため、これは別途、逆シリアル化する必要があります。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A?displayProperty=fullName> では、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> を呼び出してシリアル化された `Stream` を受け取り、そのデータを逆シリアル化するという処理が行われます。 オブジェクトを .NET でシリアル化できないなど、カスタムのシリアル化が必要な場合は、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> を使用してください。 そのような場合は、<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.Serialize%2A?displayProperty=fullName> メソッドをオーバーライドする必要があります。

 読み取り専用のビジュアライザーを作成する場合は、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A> または <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A> を使った一方向の通信で十分です。 データ オブジェクトの編集をサポートするビジュアライザーを作成する場合、それだけでは不十分です。 オブジェクト プロバイダーからオブジェクト ソースへと、データ オブジェクトを戻す機能が必要となります。 次の表は、この目的で使用される、オブジェクト プロバイダーとオブジェクト ソースの API を示しています。

|オブジェクト プロバイダー|オブジェクト ソース|
|---------------------|-------------------|
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A><br /><br /> または<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.CreateReplacementObject%2A>|

 ここでも、オブジェクト プロバイダーには、使用できる API が 2 つ存在します。 データは常に `Stream` としてオブジェクト プロバイダーからオブジェクト ソースへと送られますが、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A> の場合は、別途、オブジェクトを `Stream` にシリアル化する処理が必要となります。

 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceObject%2A> は、指定したオブジェクトを受け取り、それを `Stream` にシリアル化した後、<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A> を呼び出して、`Stream` を <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.CreateReplacementObject%2A> に送ります。

 いずれかの Replace メソッドを使用すると、視覚化対象であるオブジェクトを置き換える新しいデータ オブジェクトがデバッグ対象側に作成されます。 オブジェクトそのものを置き換えずに、元のオブジェクトの内容を変更する場合は、次の表に示した、いずれかの Transfer メソッドを使用してください。 これらの API では、視覚化対象であるオブジェクトを置き換えることなく、データが双方向で同時に転送されます。

|オブジェクト プロバイダー|オブジェクト ソース|
|---------------------|-------------------|
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.TransferData%2A><br /><br /> または<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.TransferObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.TransferData%2A>|

## <a name="see-also"></a>関連項目
- [方法: ビジュアライザーを記述する](create-custom-visualizers-of-data.md)
- [チュートリアル: C# でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [チュートリアル: Visual Basic でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [チュートリアル: Visual Basic でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [ビジュアライザーのセキュリティに関する考慮事項](../debugger/visualizer-security-considerations.md)