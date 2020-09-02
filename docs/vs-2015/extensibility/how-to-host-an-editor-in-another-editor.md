---
title: '方法: エディターを別のエディターでホストする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - host a nested editor
ms.assetid: 2b0eb705-fe94-4ca8-93e0-9dbd8ce61a44
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4d4b4ff425feb22b5057a8d1a76b7f73b8932d9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204168"
---
# <a name="how-to-host-an-editor-in-another-editor"></a>方法: エディターを別のエディターでホストする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、ホストウィンドウを親ウィンドウとして指定することで、1つのエディターを別のエディターでホストできます。 これを行うには、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> 子ウィンドウフレームにパラメーターとを設定し <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> ます。  
  
### <a name="to-set-up-the-window-frame-to-host-an-editor"></a>エディターをホストするためのウィンドウフレームを設定するには  
  
1. 子ウィンドウペインを作成することによって、エディターをホストされたエディターとして指定します。  
  
     このペインには、エディターのテキストが表示されます。  
  
2. またはメソッドを使用して、ホスティングエディターを作成し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A> ます。  
  
3. これらの <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> プロパティをパラメーターとしてメソッドに渡すことによって、ホストされるエディターのウィンドウフレームの実装でプロパティとプロパティを設定し <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A> ます。  
  
     これらのパラメーターを取得する必要がある場合は、これらのプロパティをメソッドに渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> ます。  
  
4. 含まれて <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> いるエディターに対してメソッドを呼び出します。  
  
     エディターが格納されているエディターのホストペインに表示されます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 Visual Studio Team Edition for アーキテクトの **アプリケーションデザイナー** は、別のエディターをホストしているエディターウィンドウフレームの例です。 **アプリケーションデザイナー**は、右側のウィンドウに他のデザイナーをホストします。 含まれている各デザイナーのデザイナーパネル (または [ **プロパティ** ] ページ) が、格納しているウィンドウフレームに追加されます。
