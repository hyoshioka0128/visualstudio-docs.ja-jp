---
title: '方法 : ライブラリ内のシンボルを識別する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1fe920fabd05a875b336467fbba16e4229fa9613
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708003"
---
# <a name="how-to-identify-symbols-in-a-library"></a>方法: ライブラリ内のシンボルを識別する
シンボル参照ツールは、シンボルの階層ビューを表示します。 シンボルは、名前空間、オブジェクト、クラス、クラス メンバー、およびその他の言語要素を表します。

 階層内の各シンボルは、シンボル ライブラリからオブジェクト マネージャに渡されるナビゲーション情報[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]によって、次のインターフェイスを通じて識別できます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.

 階層内のシンボルの位置は、シンボルを区別します。 シンボル参照ツールが特定のシンボルに移動できるようにします。 シンボルへの一意の完全修飾パスによって、場所が決まります。 パス内の各要素はノードです。 パスは最上位ノードから始まり、特定のシンボルで終わります。 たとえば、M1 メソッドが C1 クラスのメンバーで、C1 が N1 名前空間にある場合、M1 メソッドの完全パスは N1 になります。C1.M1. このパスには、N1、C1、M1 の 3 つのノードが含まれます。

 ナビゲーション情報により、オブジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]マネージャは、階層内のシンボルを検索、選択、および維持することができます。 これにより、あるブラウジングツールから別のブラウジングツールに移動できます。 オブジェクト**ブラウザを**使用してプロジェクト内の[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]シンボルを参照しているときに、メソッドを右クリックし、**呼び出しブラウザ**ツールを起動して、呼び出しグラフにメソッドを表示できます。

 2 つのフォームはシンボルの場所を記述します。 正規形式は、シンボルの完全修飾パスに基づいています。 これは、階層内のシンボルの一意の位置を表します。 シンボル参照ツールとは無関係です。 正規のフォーム情報を取得するには、オブジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]マネージャーはメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A>を呼び出します。 プレゼンテーション フォームは、特定のシンボル参照ツール内でのシンボルの場所を示します。 シンボルの位置は、階層内の他のシンボルの位置を基準にしています。 指定されたシンボルには複数のプレゼンテーション パスを指定できますが、正規のパスは 1 つだけです。 たとえば、C1 クラスが C2 クラスから継承され、両方のクラスが N1 名前空間にある場合、**オブジェクト ブラウザー**には次の階層ツリーが表示されます。

```
N1
    C1
        Bases and Interfaces
            C2
    C2
        Bases and Interfaces
. . . . . . . . . . .

```

 C2 クラスの正規パスは、この例では N1 + C2 です。 C2 のプレゼンテーション パスには、C1 および "ベースとインターフェイス" ノードが含まれます: N1 + C1 + "ベースとインターフェイス" + C2.

 プレゼンテーション フォーム情報を取得するために、オブジェクト マネージャ<xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A>はメソッドを呼び出します。

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>正規およびプレゼンテーション フォームの情報を取得するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> メソッドを実装します。

     オブジェクト マネージャーは、シンボルの正規のパスに含まれるノードの一覧を取得するには、このメソッドを呼び出します。

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

     オブジェクト マネージャは、シンボルのプレゼンテーション パスに含まれるノードのリストを取得するために、このメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [方法: オブジェクト マネージャーにライブラリを登録する](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
