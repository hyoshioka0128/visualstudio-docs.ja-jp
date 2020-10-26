---
title: '方法: ライブラリ内のシンボルを識別する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f154c63940189f1a6035246fb7f72ec27be677f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191873"
---
# <a name="how-to-identify-symbols-in-a-library"></a>方法: ライブラリでのシンボルの識別
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボル参照ツールは、シンボルの階層ビューを表示します。 シンボルは、名前空間、オブジェクト、クラス、クラスメンバー、およびその他の言語要素を表します。  
  
 階層内の各シンボルは、シンボルライブラリによってオブジェクトマネージャーに渡されるナビゲーション情報によって、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 次のインターフェイスを介して識別できます。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.  
  
 階層内のシンボルの場所によって、シンボルが区別されます。 これにより、シンボル参照ツールが特定のシンボルに移動できるようになります。 シンボルへの一意の完全修飾パスによって場所が決まります。 パス内の各要素はノードです。 パスは最上位ノードから始まり、特定の記号で終わります。 たとえば、M1 メソッドが C1 クラスのメンバーで、C1 が N1 名前空間にある場合、M1 メソッドの完全パスは N1 です。C1.M1. このパスには、N1、C1、および M1 の3つのノードが含まれています。  
  
 ナビゲーション情報を使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] すると、オブジェクトマネージャーは階層内のシンボルを検索、選択、および選択したままにすることができます。 ブラウズツール間を移動できます。 **オブジェクトブラウザー**を使用してプロジェクトのシンボルを参照するときに [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 、メソッドを右クリックし、**呼び出しブラウザー**ツールを起動して、呼び出し先のメソッドを表示することができます。  
  
 シンボルの場所を記述する2つの形式。 正規の形式は、シンボルの完全修飾パスに基づいています。 これは、階層内の記号の一意の位置を表します。 シンボル参照ツールに依存しません。 正規のフォーム情報を取得するために、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] オブジェクトマネージャーはメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> ます。 プレゼンテーションフォームには、特定のシンボル参照ツール内のシンボルの場所が記述されています。 記号の位置は、hierarchicy 内の他の記号の位置を基準としています。 特定のシンボルには複数のプレゼンテーションパスを含めることができますが、標準パスは1つだけです。 たとえば、C1 クラスが C2 クラスから継承され、両方のクラスが N1 名前空間にある場合、 **オブジェクトブラウザー** には次の階層ツリーが表示されます。  
  
```  
N1  
    C1  
        Bases and Interfaces  
            C2  
    C2  
        Bases and Interfaces  
. . . . . . . . . . .  
  
```  
  
 C2 クラスの正規のパス (この例では、N1 + C2)。 C2 のプレゼンテーションパスには、C1 および "基底クラスとインターフェイス" ノードが含まれています: N1 + C1 + "基底およびインターフェイス" + C2。  
  
 プレゼンテーションフォーム情報を取得するために、オブジェクトマネージャーはメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> ます。  
  
## <a name="identifying-a-symbol-in-the-hierarchy"></a>階層内のシンボルを識別する  
  
#### <a name="to-obtain-canonical-and-presentation-forms-information"></a>標準およびプレゼンテーションのフォーム情報を取得するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> メソッドを実装します。  
  
     オブジェクトマネージャーは、このメソッドを呼び出して、シンボルの正規パスに含まれるノードの一覧を取得します。  
  
    ```vb  
    Public Function EnumCanonicalNodes(ByRef ppEnum As Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes) As Integer  
        Dim EnumNavInfoNodes As CallBrowserEnumNavInfoNodes = _New CallBrowserEnumNavInfoNodes(m_strMethod)  
        ppEnum = CType(EnumNavInfoNodes, IVsEnumNavInfoNodes)  
        Return 0  
    End Function  
    ```  
  
    ```csharp  
    public int EnumCanonicalNodes(out Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes ppEnum)  
    {  
        CallBrowserEnumNavInfoNodes EnumNavInfoNodes =  
            new CallBrowserEnumNavInfoNodes(m_strMethod);  
        ppEnum = (IVsEnumNavInfoNodes)(EnumNavInfoNodes);  
        return 0;  
    }  
  
    ```  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> メソッドを実装します。  
  
     オブジェクトマネージャーは、このメソッドを呼び出して、シンボルのプレゼンテーションパスに含まれるノードの一覧を取得します。  
  
## <a name="see-also"></a>参照  
 [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)   
 [方法: オブジェクトマネージャーにライブラリを登録する](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)   
 [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
