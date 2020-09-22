---
title: '方法: エラーマーカーを実装する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - error markers
ms.assetid: e8e78514-5720-4fc2-aa43-00b6af482e38
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2af9e0765fb5bc73a35bebfc2f50f5d2a41122d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841705"
---
# <a name="how-to-implement-error-markers"></a>方法: エラー マーカーを実装する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エラーマーカー (または赤色の波下線) は、実装するテキストエディターのカスタマイズの中で最も困難です。 ただし、VSPackage のユーザーに与えられるメリットは、それを提供するコストをはるかに上回る可能性があります。 エラーマーカーは、言語パーサーによって不適切と思われるテキストを波線または波線でマークします。 このインジケーターは、プログラマが間違ったコードを視覚的に表示するのに役立ちます。  
  
 赤色の波下線を実装するには、テキストマーカーを使用します。 ルールとして、言語サービスは、アイドル状態またはバックグラウンドスレッドで、テキストバッファーに赤色の波下線をバックグラウンドパスとして追加します。  
  
### <a name="to-implement-the-red-wavy-underline-feature"></a>赤色の波下線機能を実装するには  
  
1. 赤色の波線の下に配置するテキストを選択します。  
  
2. 型のマーカーを作成 `MARKER_CODESENSE_ERROR` します。 詳細については、「 [方法: 標準テキストマーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)」を参照してください。  
  
3. その後、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> インターフェイスポインターを渡します。  
  
   このプロセスでは、特定のマーカーにヒントテキストまたは特殊なコンテキストメニューを作成することもできます。 詳細については、「 [方法: 標準テキストマーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)」を参照してください。  
  
   エラーマーカーを表示するには、次のオブジェクトが必要です。  
  
- パーサー。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2>再解析される行を識別するために、行情報の変更の記録を保持するタスクプロバイダー (の実装)。  
  
- メソッドを使用してビューからカレット変更イベントをキャプチャするテキストビューフィルター <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents.OnChangeCaretLine%2A> 。  
  
  パーサー、タスクプロバイダー、およびフィルターは、エラーマーカーを可能にするために必要なインフラストラクチャを提供します。 次の手順では、エラーマーカーを表示するプロセスについて説明します。  
  
1. フィルター処理されているビューでは、フィルターは、そのビューのデータに関連付けられているタスクプロバイダーへのポインターを取得します。  
  
    > [!NOTE]
    > メソッドのヒント、ステートメント入力候補、エラーマーカーなどに対して同じコマンドフィルターを使用できます。  
  
2. 別の行に移動したことを示すイベントをフィルターが受信すると、エラーを確認するためのタスクが作成されます。  
  
3. タスクハンドラーは、行がダーティかどうかを確認します。 その場合は、エラーの行を解析します。  
  
4. エラーが検出された場合、タスクプロバイダーはタスク項目インスタンスを作成します。 このインスタンスは、環境がテキストビューのエラーマーカーとして使用するテキストマーカーを作成します。  
  
## <a name="see-also"></a>参照  
 [レガシ API でのテキストマーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [方法: 標準テキストマーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)   
 [方法: カスタムテキストマーカーを作成する](../extensibility/how-to-create-custom-text-markers.md)   
 [方法: テキスト マーカーを使用する](../extensibility/how-to-use-text-markers.md)
