---
title: '方法: ライブラリ内のシンボルを識別する |Microsoft Docs'
description: シンボルライブラリから Visual Studio オブジェクトマネージャーにナビゲーション情報を渡すメソッドを実装することによって、ライブラリ内のシンボルを識別する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4b1dab9dc6bee4ed987141057194d8b00ff35f99
ms.sourcegitcommit: 2f964946d7044cc7d49b3fc10b413ca06cb2d11b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761378"
---
# <a name="how-to-identify-symbols-in-a-library"></a>方法: ライブラリ内のシンボルを識別する
シンボル参照ツールは、シンボルの階層ビューを表示します。 シンボルは、名前空間、オブジェクト、クラス、クラスメンバー、およびその他の言語要素を表します。

 階層内の各シンボルは、シンボルライブラリによってオブジェクトマネージャーに渡されるナビゲーション情報によって、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 次のインターフェイスを介して識別できます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.

 階層内のシンボルの場所によって、シンボルが区別されます。 これにより、シンボル参照ツールが特定のシンボルに移動できるようになります。 シンボルへの一意の完全修飾パスによって場所が決まります。 パス内の各要素はノードです。 パスは最上位ノードから始まり、特定の記号で終わります。 たとえば、M1 メソッドが C1 クラスのメンバーで、C1 が N1 名前空間にある場合、M1 メソッドの完全パスは N1 です。C1.M1. このパスには、N1、C1、および M1 の3つのノードが含まれています。

 オブジェクトマネージャーは、ナビゲーション情報を使用して、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 階層内のシンボルを検索、選択、および選択したままにすることができます。 ブラウズツール間を移動できます。 **オブジェクトブラウザー** を使用してプロジェクトのシンボルを参照するときに [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 、メソッドを右クリックし、**呼び出しブラウザー** ツールを起動して、呼び出し先のメソッドを表示することができます。

 シンボルの場所を記述する2つの形式。 正規の形式は、シンボルの完全修飾パスに基づいています。 これは、階層内の記号の一意の位置を表します。 シンボル参照ツールに依存しません。 正規のフォーム情報を取得するために、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクトマネージャーはメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> ます。 プレゼンテーションフォームには、特定のシンボル参照ツール内のシンボルの場所が記述されています。 シンボルの位置は、階層内の他の記号の位置を基準としています。 特定のシンボルには複数のプレゼンテーションパスを含めることができますが、標準パスは1つだけです。 たとえば、C1 クラスが C2 クラスから継承され、両方のクラスが N1 名前空間にある場合、 **オブジェクトブラウザー** には次の階層ツリーが表示されます。

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

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>標準およびプレゼンテーションのフォーム情報を取得するには

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

## <a name="see-also"></a>関連項目
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [方法: オブジェクトマネージャーにライブラリを登録する](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクトマネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
