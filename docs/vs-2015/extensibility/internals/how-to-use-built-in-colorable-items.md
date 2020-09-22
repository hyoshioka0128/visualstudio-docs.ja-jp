---
title: '方法: 組み込みの装飾 Items | を使用するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a86361f28eb4c73a65093fc5c80ef15ddf791a77
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841473"
---
# <a name="how-to-use-built-in-colorable-items"></a>方法: ビルトインの配色可能な項目の使用
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

組み込みの装飾項目を使用する前に、まず、独自のカスタム装飾項目 (この場合はオブジェクト) を提供しないことを統合開発環境 (IDE) に通知する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> ます。 これを行うには、言語サービスのレジストリエントリを設定します。  
  
### <a name="to-use-built-in-colorable-items"></a>組み込みの装飾アイテムを使用するには  
  
1. HKEY_LOCAL_MACHINE \VisualStudio \\ *X.Y*\Languages\Language Services \\ の*言語名*を使用します。ここで、 *X.y*はのバージョンであり、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] *言語名*は言語の名前です。という DWORD レジストリエントリの値を作成し `RequestStockColors` ます。  
  
2. `RequestStockColors`レジストリエントリの値を1に設定します。  
  
     レジストリエントリを作成した後は、その <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 列挙体のメンバーを使用して、 <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> エディターで使用する色属性の配列を入力できます。  
  
    > [!NOTE]
    > カスタム装飾項目を指定する場合は、このレジストリエントリを設定しないでください。 詳細については、「 [Custom 装飾 Items](../../extensibility/internals/custom-colorable-items.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カスタムエディターでの構文の色分け](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [実装 (構文の色分けを)](../../extensibility/internals/implementing-syntax-coloring.md)   
 [カスタム装飾項目](../../extensibility/internals/custom-colorable-items.md)   
 [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service2.md)
