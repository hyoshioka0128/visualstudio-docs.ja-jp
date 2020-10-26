---
title: '方法: エディターがフォーカスを失ったときにイベントを発生させる |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - fire events on losing focus
ms.assetid: 64d40695-6917-468a-8037-a253453ac159
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ebca733798636ca32787b88b8874c31a2ffffdb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204194"
---
# <a name="how-to-fire-events-when-the-editor-loses-focus"></a>方法: エディターでフォーカスが失われたときにイベントを発生させる
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

場合によっては、エディターがウィンドウフレームにフォーカスを失ったタイミングを知る必要があります。 たとえば、エディターがフォーカスを失った後にコードウィンドウからコードを抽出することが必要になる場合があります。 次の手順では、エディターがフォーカスを失ったときの通知を受信する手順を説明します。  
  
### <a name="to-fire-an-event-in-response-to-an-editor-losing-focus"></a>エディターがフォーカスを失ったときにイベントを発生させるには  
  
1. からオブジェクトを取得して、選択イベントを監視 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> します。  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.AdviseSelectionEvents%2A>を呼び出し、オブジェクトを指定し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents> ます。  
  
3. の呼び出しで <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> 、を探し `elementid==SEID_WindowFrame` ます。  
  
4. `varValueNew`次の2つの点についてパラメーターをテストします。  
  
    1. 検索しているウィンドウフレーム。  
  
    2. プログラムがウィンドウフレームの選択範囲を失ったポイント。
