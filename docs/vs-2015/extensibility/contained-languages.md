---
title: 含まれている言語 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - contained languages
ms.assetid: b75bbb51-8e42-41b1-bece-09ab0b1f03cc
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0920999eee7460c8bf697e245bae55a3641b8e18
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184286"
---
# <a name="contained-languages"></a>含まれている言語
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)] 

*含ま* れている言語は、他の言語に含まれる言語です。 たとえば、ページの HTML に [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] [!INCLUDE[csprcs](../includes/csprcs-md.md)] はまたはスクリプトを含めることができ [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ます。 .Aspx ファイルエディターでは、HTML とスクリプト言語の両方に対して IntelliSense、色付け、およびその他の編集機能を提供するために、二重言語アーキテクチャが必要です。  
  
## <a name="implementation"></a>実装  
 含まれている言語に実装する必要がある最も重要なインターフェイスは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> インターフェイスです。 このインターフェイスは、第一言語でホストできる任意の言語によって実装されます。 これにより、言語サービスの colorizer、テキストビューフィルター、および主言語サービス ID にアクセスできるようになります。 を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory> 使用すると、インターフェイスを作成でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> ます。 次の手順は、含まれている言語を実装する方法を示しています。  
  
1. `QueryService()`言語サービス id とのインターフェイス id を取得するには、を使用し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory> ます。  
  
2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory.GetLanguage%2A>インターフェイスを作成するには、メソッドを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>インターフェイス、1つ以上の[項目 id](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>) 、およびインターフェイスを渡し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator> ます。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>インターフェイス (テキストバッファーコーディネーターオブジェクト) は、プライマリファイル内の場所をセカンダリ言語のバッファーにマップするために必要な基本的なサービスを提供します。  
  
     たとえば、1つの .aspx ファイルで、プライマリファイルには、ASP、HTML、および含まれるすべてのコードが含まれます。 ただし、セカンダリバッファーは、含まれているコードだけをクラス定義と共に使用して、セカンダリバッファーに有効なコードファイルを作成します。 バッファーコーディネーターは、あるバッファーから別のバッファーへの編集を調整する作業を処理します。  
  
4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A>プライマリ言語であるメソッドは、バッファーコーディネーターに対し、バッファー内のテキストをセカンダリバッファー内の対応するテキストにマップするように指示します。  
  
     この言語は、 <xref:Microsoft.VisualStudio.TextManager.Interop.NewSpanMapping> 現在プライマリとセカンダリスパンのみを含む構造体の配列を渡します。  
  
5. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapPrimaryToSecondarySpan%2A>メソッドとメソッドは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapSecondaryToPrimarySpan%2A> プライマリバッファーとセカンダリバッファーの間のマッピングを提供します。
