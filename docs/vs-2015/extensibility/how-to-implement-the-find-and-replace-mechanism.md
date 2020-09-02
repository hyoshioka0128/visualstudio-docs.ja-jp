---
title: '方法: 検索と置換の機構を実装する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - find and replace
ms.assetid: bbd348db-3d19-42eb-99a2-3e808528c0ca
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d4362d0b0c3f013ce6f38d13265dcc181c77012c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62548697"
---
# <a name="how-to-implement-the-find-and-replace-mechanism"></a>方法: 検索と置換のメカニズムを実装する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio には、検索と置換を実装する2つの方法が用意されています。 1つの方法は、テキストイメージをシェルに渡し、検索、強調表示、およびテキストの置換を処理できるようにすることです。 これにより、ユーザーは複数のテキスト範囲を指定できます。 または、VSPackage がこの機能自体を制御できます。 どちらの場合も、開いているすべてのドキュメントの現在のターゲットとターゲットについてシェルに通知する必要があります。  
  
### <a name="to-implement-findreplace"></a>検索と置換を実装するには  
  
1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>フレームプロパティまたはによって返されるいずれかのオブジェクトにインターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> ます。 カスタムエディターを作成する場合は、カスタムエディタークラスの一部としてこのインターフェイスを実装する必要があります。  
  
2. メソッドを使用して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.GetCapabilities%2A> エディターがサポートするオプションを指定し、テキストイメージ検索を実装するかどうかを指定します。  
  
     エディターがテキストイメージの検索をサポートしている場合は、を実装 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.GetSearchImage%2A> します。  
  
     それ以外の場合は、およびを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A> ます。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A>メソッドとメソッドを実装すると <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A> 、インターフェイスを呼び出すことによって検索タスクを簡略化でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindHelper> ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindHelper>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.GetSearchImage%2A>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
