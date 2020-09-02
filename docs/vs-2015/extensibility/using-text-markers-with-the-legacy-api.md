---
title: レガシ API でテキストマーカーを使用する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text markers
ms.assetid: 937a0b19-1216-45d5-a7ad-4fe1d6f73097
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3dff5e6ecf60d389730841e99b87db584465e020
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695475"
---
# <a name="using-text-markers-with-the-legacy-api"></a>レガシ API でのテキスト マーカーの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストマーカーは、テキスト領域の表示と動作に影響を与える可能性があるバッファー内のテキストの浮動範囲です。 マーカーには、ブレークポイント、ブックマーク、波線、および読み取り専用の領域が含まれます。 テキストマーカーは、基本的に構文の色分けとは異なります。 構文の色分けを使用すると、テキスト領域に関連付けられている言語の構文を簡単に伝えることができます。 一般的に、Windows が画面を再描画するときに、速度が重要な場合に、構文の色分けが要求されます。 構文の色分けでは、テキストの色のみが変更されます。 テキストマーカーは、他の多くのテキストプロパティを変更できます。 テキストマーカーは、"フローティング" し、特殊な動作と色分けを適用できます。  
  
 テキストマーカーに関連するパフォーマンスのオーバーヘッドのため、テキストバッファー用に多くのマーカーを作成しないでください。 各マーカーは、ユーザーがバッファーの内容を編集するたびに更新されます。  
  
> [!NOTE]
> ユーザーは、表示されているマーカーの種類の色を変更できますが、図形とスタイルは変更できません。 詳細については、「[ [フォントおよび色] ([オプション] ダイアログボックス](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)-[環境])」を参照してください。  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[方法: 標準のテキスト マーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)|コアエディターによって提供される標準のテキストマーカーの種類をテキストビューに追加する方法について説明し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。|  
|[方法: エラー マーカーを実装する](../extensibility/how-to-implement-error-markers.md)|赤色の波下線を使用して [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] エラーを示すために使用されるマーカーのインスタンスを実装する方法について説明します。|  
|[方法: カスタム テキスト マーカーを作成する](../extensibility/how-to-create-custom-text-markers.md)|テキストビューにカスタムのテキストマーカーの種類を作成して追加する方法について説明します。|  
|[方法: テキスト マーカーを使用する](../extensibility/how-to-use-text-markers.md)|テキストマーカーを追加する方法について説明します。|  
|[コア エディターの内部](../extensibility/inside-the-core-editor.md)|コアエディターの機能について説明し、コアエディターをカスタマイズする方法の詳細について説明します。|  
|[エディターの機能](https://msdn.microsoft.com/bdac940d-1f14-4019-a01f-fd0bb3dc7198)|コアエディターで使用できる機能について説明し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。|  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>  
 特定のテキストマーカーの種類に関する情報を取得するための統一されたメカニズムを提供します。これは、エディターによって定義済みであるか、VSPackage によって登録されます。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLineMarker>  
 2次元座標を使用して、テキストバッファー内のテキストマーカーの位置へのアクセスを提供し、その位置を調整します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>  
 テキストマーカーを管理するためのメソッドを提供します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]テキストマーカーの調整に使用される IDE およびその他のプロセスへのコールバックを提供します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced>  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>追加のコールバックを提供することによって、インターフェイスを通じて使用できる機能を拡張します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>追加のコールバックを提供することによって、インターフェイスを通じて使用できる機能を拡張します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerColorSet>  
 マーカーの種類を有効にして、他のマーカーの種類が同じ色のセットを共有するかどうかを判断します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>  
 コアエディターのテキストマーカーのコンテキストを提供します。 コアエディターに含まれるテキストマーカーの種類ごとに、IDE によって別のオブジェクトが作成され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> ます。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerGlyphDropHandler>  
 ドラッグアンドドロップ編集をサポートするグリフを持つマーカーに対して提供されるハンドラー。 グリフは、マーカーの位置を示すアイコンです。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>他の vspackage にテキストマーカーを提供する、サービスからのインターフェイスを返します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamMarker>  
 1次元座標を使用して、テキストバッファー内のテキストマーカーの位置へのアクセスを提供し、その位置を調整します。 可能な場合は、このインターフェイスを使用しないでください。
