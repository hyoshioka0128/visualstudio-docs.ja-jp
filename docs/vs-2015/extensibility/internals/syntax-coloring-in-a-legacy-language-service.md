---
title: 従来の言語サービスでの構文の色分け |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 59d25c338cb0c7406c533afeceaf3675fbd16e96
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841933"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>従来の言語サービスでの構文の色分け表示
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、色分けサービスを使用して言語の要素を識別し、エディターで指定された色でそれらを表示します。  
  
## <a name="colorizer-model"></a>Colorizer モデル  
 言語サービスは、この <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを実装します。このインターフェイスは、エディターによって使用されます。 この実装は、次の図に示すように、言語サービスとは別のオブジェクトです。  
  
 ![SVC Colorizer グラフィック](../../extensibility/internals/media/figlgsvccolorizer.gif "FigLgSvcColorizer")  
単純な colorizer モデル  
  
> [!NOTE]
> 構文の色分け表示サービスは、色分けテキストの一般的なメカニズムとは別のものです [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 色分けをサポートする一般的なメカニズムの詳細については [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 、「 [フォントおよび色の使用](../../extensibility/using-fonts-and-colors.md)」を参照してください。  
  
 また、言語サービスでは、カスタムの装飾項目を提供することを通知することで、エディターで使用されるカスタム装飾項目を指定できます。 これを行うには、インターフェイスを <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 実装するのと同じオブジェクトにインターフェイスを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> ます。 このメソッドは、エディターがメソッドを呼び出したときにカスタム装飾項目の数を返し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> エディターがメソッドを呼び出したときに個々のカスタム装飾項目を返し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> ます。  
  
 メソッドは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> インターフェイスを実装するオブジェクトを返し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> ます。 言語サービスで24ビットまたは高色の値がサポートされている場合は、インターフェイス <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> と同じオブジェクトにインターフェイスを実装する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> ます。  
  
## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VSPackage が言語サービスカラーを使用する方法  
  
1. VSPackage は、適切な言語サービスを取得する必要があります。そのためには、言語サービス VSPackage で次の操作を行う必要があります。  
  
    1. インターフェイスを実装するオブジェクトを使用し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> て、色分けされたテキストを取得します。  
  
         通常、テキストは、インターフェイスを実装するオブジェクトを使用して表示され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。  
  
    2. 言語サービスの GUID を取得するには、VSPackage のサービスプロバイダーに対してクエリを実行します。 言語サービスは、レジストリのファイル拡張子によって識別されます。  
  
    3. メソッドを呼び出して、言語サービスをに関連付け <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> ます。  
  
2. VSPackage は、次のように colorizer オブジェクトを取得して使用できるようになりました。  
  
    > [!NOTE]
    > コアエディターを使用する Vspackage では、言語サービスの colorizer オブジェクトを明示的に取得する必要はありません。 コアエディターのインスタンスは、適切な言語サービスを取得するとすぐに、ここに示されているすべての色付けタスクを実行します。  
  
    1. 言語サービス `T:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer` <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> のオブジェクトに対してメソッドを呼び出すことによって、、の各インターフェイスを実装する言語サービスの colorizer いるオブジェクトを取得し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> ます。  
  
    2. メソッドを呼び出して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 、テキストの特定の範囲の色の情報を取得します。  
  
         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 色分けされたテキスト範囲内の文字ごとに1つずつ、値の配列を返します。 値は、コアエディターによって管理される既定の装飾 item リスト、または言語サービス自体によって管理されるカスタム装飾項目リストの装飾 item リストにインデックスが付けられます。  
  
    3. 選択したテキストを表示するには、メソッドによって返される色付け情報を使用し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> ます。  
  
> [!NOTE]
> 言語サービスの colorizer を使用するだけでなく、汎用テキストの色分け機構を使用することもでき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 このメカニズムの詳細については、「 [フォントおよび色の使用](../../extensibility/using-fonts-and-colors.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [構文の色分け表示の実装](../../extensibility/internals/implementing-syntax-coloring.md)  
 エディターが言語サービスの構文の色分けにアクセスする方法と、構文の色分けをサポートするために言語サービスが実装する必要がある内容について説明します。  
  
 [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)  
 言語サービスの組み込みの装飾項目を使用する方法を示します。  
  
 [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)  
 カスタム装飾項目を実装する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [フォントと色の使用](../../extensibility/using-fonts-and-colors.md)
