---
title: データのカスタムビジュアライザーを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.visualizer.troubleshoot
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
- visualizers
ms.assetid: c24c006f-f2ac-429f-89db-677fc0c6e1ea
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 50df868f0e01d49d4c49bccae32d743d5291a066
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842044"
---
# <a name="create-custom-visualizers-of-data"></a>データのカスタムビジュアライザーを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ビジュアライザーは、デバッガーの [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] ユーザーインターフェイスのコンポーネントです。 *ビジュアライザー*は、データ型に適した方法で変数またはオブジェクトを表示するダイアログボックスまたは別のインターフェイスを作成します。 たとえば、HTML ビジュアライザーは、HTML 文字列を解釈し、ブラウザー ウィンドウに表示されるとおりに結果を表示します。また、ビットマップ ビジュアライザーは、ビットマップ構造体を解釈し、ビットマップが表すグラフィックを表示します。 一部のビジュアライザーでは、データを表示するだけでなく、変更することもできます。  
  
 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] デバッガーには、6 つの標準的なビジュアライザーが用意されています。 テキスト ビジュアライザー、HTML ビジュアライザー、XML ビジュアライザー、JSON ビジュアライザー: これらのすべてが文字列オブジェクトを処理します。WPF ツリー ビジュアライザー: WPF オブジェクトのビジュアル ツリーのプロパティを表示します。データセット ビジュアライザー: DataSet オブジェクト、DataView オブジェクト、および DataTable オブジェクトを処理します。 その他のビジュアライザーは、今後 Microsoft Corporation からダウンロード可能になる場合があり、サード パーティやコミュニティからも入手できます。 また、独自のビジュアライザーを記述して、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] デバッガーにインストールすることもできます。  
  
> [!NOTE]
> **ストア**アプリでは、標準のテキスト、HTML、XML、および JSON ビジュアライザーのみがサポートされています。 カスタム (ユーザーが作成した) ビジュアライザーはサポートされていません。  
  
 デバッガーでは、ビジュアライザーは虫眼鏡アイコンで表されます。 データ **ヒント**に虫眼鏡アイコンが表示されている場合、[デバッガー変数] ウィンドウ、または [ **クイックウォッチ** ] ダイアログボックスで虫眼鏡をクリックすると、対応するオブジェクトのデータ型に適したビジュアライザーを選択できます。  
  
 ビジュアライザーは、.NET Compact Framework ではサポートされていません。  
  
> [!NOTE]
> デバッガー ビジュアライザーでは、部分信頼アプリケーションが許可する以上の特権が必要です。 この結果、部分信頼コードで動作が停止した場合、ビジュアライザーは読み込まれません。 ビジュアライザーを使用してデバッグするには、完全信頼コードを実行する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: ビジュアライザーを記述する](../debugger/how-to-write-a-visualizer.md)  
  
 [チュートリアル: C# でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)  
  
 [方法: ビジュアライザーをインストールする](../debugger/how-to-install-a-visualizer.md)  
  
 [方法: ビジュアライザーをテストおよびデバッグする](../debugger/how-to-test-and-debug-a-visualizer.md)  
  
 [ビジュアライザー API リファレンス](../debugger/visualizer-api-reference.md)  
  
## <a name="related-sections"></a>関連項目  
 [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
