---
title: 従来の API を使用して言語サービスコンテキストを提供する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language service context
ms.assetid: daa2df22-9181-4bad-b007-a7d40302bce1
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4471b71b612008ba7d0733c92286415cd3c3f6b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193874"
---
# <a name="providing-a-language-service-context-by-using-the-legacy-api"></a>レガシ API を使用する言語サービス コンテキストの提供
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コアエディターを使用してユーザーコンテキストを提供する言語サービスには [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、テキストマーカーコンテキストを提供する方法と、すべてのユーザーコンテキストを指定する方法の2つのオプションがあります。 それぞれの違いについては、ここで説明します。  
  
 独自のエディターに接続されている言語サービスにコンテキストを提供する方法の詳細については、「 [方法: エディターのコンテキストを指定](../extensibility/how-to-provide-context-for-editors.md)する」を参照してください。  
  
## <a name="provide-text-marker-context-to-the-editor"></a>テキストマーカーコンテキストをエディターに提供する  
 コアエディターのテキストマーカーによって示されるコンパイラエラーのコンテキストを提供するには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インターフェイスを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> ます。 このシナリオでは、言語サービスは、カーソルがテキストマーカー上にある場合にのみコンテキストを提供します。 これにより、エディターは、カーソル位置に属性なしでキーワードを **動的ヘルプ** ウィンドウに渡すことができます。  
  
## <a name="provide-all-user-context-to-the-editor"></a>すべてのユーザーコンテキストをエディターに提供する  
 言語サービスを作成していて、コアエディターを使用している場合は、インターフェイスを実装して、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> 言語サービスのコンテキストを提供できます。  
  
 の実装では `IVsLanguageContextProvider` 、コンテキストバッグ (コレクション) がエディターにアタッチされます。これは、コンテキストバッグの更新を担当します。 [ **ダイナミックヘルプ** ] ウィンドウが <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.Update%2A> アイドル時にこのコンテキストバッグのインターフェイスを呼び出すと、コンテキストバッグはエディターに更新プログラムを照会します。 エディターは、エディターを更新する必要があることを言語サービスに通知し、コンテキストバッグへのポインターを渡します。 これを行うには、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider.UpdateLanguageContext%2A> エディターから言語サービスに対してメソッドを呼び出します。 コンテキストバッグへのポインターを使用して、言語サービスで属性とキーワードを追加および削除できるようになりました。 詳細については、「<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>」を参照してください。  
  
 を実装するには、次の2つの方法があり `IVsLanguageContextProvider` ます。  
  
- コンテキストバッグにキーワードを指定する  
  
   コンテキストバッグを更新するためにエディターが呼び出されたときに、適切なキーワードと属性を渡し、を返し `S_OK` ます。 この戻り値は、カーソルでコンテキストバッグにキーワードを指定するのではなく、キーワードと属性コンテキストを保持するようエディターに指示します。  
  
- キーワードからキーワードを取得します。  
  
   コンテキストバッグを更新するためにエディターが呼び出されたときに、適切な属性を渡し、を返し `E_FAIL` ます。 この戻り値は、コンテキストバッグで属性を保持するようエディターに指示しますが、カーソルでキーワードを使用してコンテキストバッグを更新します。  
  
  次の図は、を実装する言語サービスに対してコンテキストがどのように提供されるかを示して `IVsLanguageContextProvider` います。  
  
  ![LangServiceImplementation2 グラフィック](../extensibility/media/vslanguageservice2.gif "vsLanguageService2")  
  言語サービスのコンテキスト  
  
  図に示すように、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] コアテキストエディターにはコンテキストバッグが添付されています。 このコンテキストバッグは、言語サービス、既定のエディター、およびテキストマーカーという3つの別個の subcontext バッグを指しています。 言語サービスとテキストマーカー subcontext バッグには、インターフェイスが実装されている場合は言語サービスの属性とキーワードが、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> インターフェイスが実装されている場合はテキストマーカーが含まれ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> ます。 これらのインターフェイスのいずれかを実装しない場合、エディターは、既定のエディター subcontext バッグのカーソルにキーワードのコンテキストを提供します。  
  
## <a name="context-guidelines-for-editors-and-designers"></a>エディターとデザイナーのコンテキストガイドライン  
 デザイナーとエディターは、エディターまたはデザイナーウィンドウの全般キーワードを指定する必要があります。 これは、ユーザーが F1 キーを押したときに、デザイナーまたはエディターに対して一般的なヘルプトピックが表示されるようにするために行われます。 また、エディターでは、カーソルに現在のキーワードを指定するか、現在の選択内容に基づいてキー用語を指定する必要があります。 これにより、ユーザーが F1 キーを押したときに表示または選択されたテキストまたは UI 要素のヘルプトピックが表示されるようになります。 デザイナーは、フォーム上のボタンなど、デザイナーで選択された項目のコンテキストを提供します。 また、エディターとデザイナーは、「 [従来の言語サービスの基本](../extensibility/internals/legacy-language-service-essentials.md)事項」に記載されている言語サービスにも接続する必要があります。
