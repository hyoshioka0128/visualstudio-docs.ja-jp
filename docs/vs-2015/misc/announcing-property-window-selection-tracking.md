---
title: プロパティウィンドウの選択の追跡の発表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], property pages support
- property pages, tracking selection
- Properties window, tracking selection
- selection, tracking
- editors [Visual Studio SDK], Properties window support
ms.assetid: a7536f82-afd7-4894-9a60-84307fb92b7e
caps.latest.revision: 13
manager: jillfra
ms.openlocfilehash: 6296993d3a1f5039024556f09b721daa82ca4f53
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "63002454"
---
# <a name="announcing-property-window-selection-tracking"></a>プロパティ ウィンドウの選択の追跡の発表
[ **プロパティ** ] ウィンドウまたはプロパティページ (フォーム、テキスト、また **はプロパティを** 表示する選択など) を操作する場合は、選択の調整方法についての完全な知識が必要です。 たとえば、1つの選択または複数の選択があるかどうかを確認する必要があります。 次に、インターフェイスを使用して、選択した型 (1 つまたは複数) を IDE に通知する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> ます。 このインターフェイスは、[ **プロパティ** ] ウィンドウで必要な情報を提供します。  
  
### <a name="to-announce-selection-to-the-environment"></a>環境に対して選択をアナウンスするには  
  
1. `QueryInterface`を呼び出し <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> ます。  
  
    1. これを行うには、作成時にビューに渡されるサイトポインターを使用します。  
  
    2. `QueryService`サービスのビューからを呼び出し `SID_STrackSelection` ます。  
  
         これにより、へのポインターが返さ <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> れます。  
  
2. 選択が変更されるたびにメソッドを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> を実装するオブジェクトへのポインターを渡し <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます。  
  
     選択コンテナーオブジェクトは、1つまたは複数の選択を使用でき、オブジェクトの選択情報を含み `IDispatch` ます。 メソッドを呼び出すと、 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 選択内容が変更されたことが [ **プロパティ** ] ウィンドウに通知されます。 次に、[ **プロパティ** ] ウィンドウで、のオブジェクトを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 1 つまたは複数の選択が発生したかどうか、および実際のオブジェクトの選択内容を確認します。  
  
     複数の選択項目を指定した場合、[ **プロパティ** ] ウィンドウでは、オブジェクトの共通プロパティ間の交差部分が検索されます。 1つのオブジェクトの選択を指定すると、[ **プロパティ** ] ウィンドウに、1つのオブジェクトのすべてのプロパティが表示されます。  
  
## <a name="see-also"></a>参照  
 [プロパティの拡張](../extensibility/internals/extending-properties.md)   
 [[プロパティ ページ]](../extensibility/internals/property-pages.md)