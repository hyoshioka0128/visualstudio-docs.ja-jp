---
title: Visual Studio 相互運用機能アセンブリパラメーターのマーシャリング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting Visual Studio SDK interop assemblies
- interop assemblies, parameter marshaling
- interop assemblies, troubleshooting
ms.assetid: 89123eae-0fef-46d5-bd36-3d2a166b14e3
caps.latest.revision: 24
manager: jillfra
ms.openlocfilehash: ac95c40b356c542da323a3ea3744827087f2d840
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686922"
---
# <a name="visual-studio-interop-assembly-parameter-marshaling"></a>Visual Studio 相互運用機能アセンブリのパラメーター マーシャリング
マネージコードで記述された Vspackage は、を呼び出すか、アンマネージ COM コードによって呼び出される必要があります。 通常、メソッドの引数は、相互運用マーシャラーによって自動的に変換またはマーシャリングされます。 ただし、引数を単純な方法で変換することはできません。 そのような場合は、相互運用機能アセンブリメソッドプロトタイプのパラメーターを使用して、COM 関数のパラメーターをできるだけ厳密に一致させることができます。 詳細については、「[相互運用マーシャリング](https://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)」を参照してください。  
  
## <a name="general-suggestions"></a>一般的な提案  
  
##### <a name="read-the-reference-documentation"></a>リファレンスドキュメントを読む  
 相互運用性の問題を検出する効果的な方法は、各メソッドのリファレンスドキュメントを参照することです。  
  
 各メソッドのリファレンスドキュメントには、関連する3つのセクションが含まれています。  
  
- [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]COM 関数プロトタイプ。  
  
- 相互運用機能アセンブリメソッドのプロトタイプ。  
  
- COM パラメーターの一覧とそれぞれの簡単な説明。  
  
##### <a name="look-for-differences-between-the-two-prototypes"></a>2つのプロトタイプ間の相違点を検索する  
 ほとんどの相互運用性の問題は、COM インターフェイス内の特定の型の定義と相互運用機能アセンブリ内の同じ型の定義との間の不一致から派生し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 たとえば、 `null` [out] パラメーターに値を渡す機能の違いについて考えてみます。 2つのプロトタイプの違いを調べて、データが渡される際の影響を考慮する必要があります。  
  
##### <a name="read-the-parameter-definitions"></a>パラメーターの定義を読み取ります。  
 パラメーターの定義を読み取ります。 COM は、1つのパラメーターに異なる種類のデータを混在させることに関する共通言語ランタイム (CLR) よりも厳格です。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]COM インターフェイスは、この柔軟性を最大限に活用します。 ポインターパラメーターの定数値など、標準以外の値またはデータ型のデータを渡すことができるパラメーターは、ドキュメントに記載されているように記述する必要があります。  
  
### <a name="iunknown-objects-passed-as-type-void"></a>型 void * * として渡された IUnknown オブジェクト  
 COM インターフェイスで型として定義されている `void **` が、 `[``iid_is``]` [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 相互運用機能アセンブリメソッドプロトタイプでとして定義されている [out] パラメーターを検索します。  
  
 場合によっては、COM インターフェイスによってオブジェクトが生成さ `IUnknown` れ、com インターフェイスによって型として渡さ `void **` れます。 これらのインターフェイスは、変数が IDL で [out] として定義されている場合、 `IUnknown` オブジェクトはメソッドを使用して参照カウントされるため、特に重要です `AddRef` 。 オブジェクトが正しく処理されない場合、メモリリークが発生します。  
  
> [!NOTE]
> `IUnknown`COM インターフェイスによって作成され、[out] 変数で返されるオブジェクトは、明示的に解放されていない場合にメモリリークを発生させます。  
  
 このようなオブジェクトを処理するマネージメソッドは、 <xref:System.IntPtr> オブジェクトへのポインターとして処理し、メソッドを呼び出してオブジェクトを取得する必要があり `IUnknown` <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> ます。 その後、呼び出し元は、戻り値を適切な型にキャストする必要があります。 オブジェクトが不要になった場合は、 <xref:System.Runtime.InteropServices.Marshal.Release%2A> を呼び出して解放します。  
  
 メソッドを呼び出し、オブジェクトを正しく処理する例を次に示し <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A> `IUnknown` ます。  
  
```  
MyClass myclass;  
Object object;  
IntPtr pObj;  
Guid iid = Typeof(MyClass).Guid;  
int hr = windowFrame.QueryViewInterface(ref iid, out pObj);     
if (NativeMethods.Succeeded(hr))   
{  
    try   
    {  
        object = Marshal.GetObjectForIUnknown(pObj);  
        myclass = object;  
    }  
    finally   
    {  
        Marshal.Release(pObj);  
    }  
}  
else   
{  
    // error calling QueryViewInterface  
}  
```  
  
> [!NOTE]
> 次のメソッドは、 `IUnknown` オブジェクトポインターを型として渡すことがわかってい <xref:System.IntPtr> ます。 このセクションで説明されているように処理します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>  
  
### <a name="optional-out-parameters"></a>省略可能な [out] パラメーター  
 COM インターフェイスで [out] データ型 (、など) として定義されているパラメーターを検索し `int` `object` ますが、これは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 相互運用機能アセンブリメソッドプロトタイプで同じデータ型の配列として定義されています。  
  
 などの一部の COM インターフェイスで <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> は、[out] パラメーターをオプションとして扱います。 オブジェクトが不要な場合、これらの COM インターフェイスは、 `null` [out] オブジェクトを作成するのではなく、そのパラメーターの値としてポインターを返します。 これは仕様です。 これらのインターフェイスでは、 `null` ポインターは VSPackage の正しい動作の一部と見なされ、エラーは返されません。  
  
 CLR では [out] パラメーターの値をにすることが許可されていないため `null` 、これらのインターフェイスのデザインされた動作の一部をマネージコード内で直接使用することはできません。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]影響を受けるインターフェイスの相互運用機能アセンブリメソッドは、関連するパラメーターを配列として定義することで問題を回避します。これは、CLR が配列を渡すことができるため `null` です。  
  
 これらのメソッドのマネージ実装は、 `null` 返されるものがない場合に、配列をパラメーターに配置する必要があります。 それ以外の場合は、正しい型の1つの要素から成る配列を作成し、戻り値を配列に格納します。  
  
 省略可能な [out] パラメーターを使用してインターフェイスから情報を受け取るマネージメソッドは、パラメーターを配列として受け取ります。 配列の最初の要素の値を確認するだけです。 それ以外の場合は `null` 、最初の要素を元のパラメーターとして扱います。  
  
### <a name="passing-constants-in-pointer-parameters"></a>ポインターパラメーターでの定数の引き渡し  
 COM インターフェイスで [in] ポインターとして定義されているが、 <xref:System.IntPtr> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 相互運用機能アセンブリのメソッドプロトタイプで型として定義されているパラメーターを探します。  
  
 同様の問題は、COM インターフェイスがオブジェクトポインターではなく、0、-1、または–2などの特別な値を渡した場合にも発生します。 とは異なり [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 、CLR では、定数をオブジェクトとしてキャストすることはできません。 代わりに、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 相互運用機能アセンブリがパラメーターを型として定義し <xref:System.IntPtr> ます。  
  
 これらのメソッドのマネージ実装では、 <xref:System.IntPtr> クラスにコンストラクターとコンストラクターの両方が含まれており、必要に応じ `int` `void *` <xref:System.IntPtr> てオブジェクトまたは整数定数からが作成されるという事実を活用する必要があります。  
  
 この型のパラメーターを受け取るマネージメソッドでは、 <xref:System.IntPtr> 型変換演算子を使用して結果を処理する必要があり <xref:System.IntPtr> ます。 まず <xref:System.IntPtr> をに変換 `int` し、関連する整数定数に対してテストします。 一致する値がない場合は、必要な型のオブジェクトに変換して続行します。  
  
 この例については、「」および「」を参照してください <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A> 。  
  
### <a name="ole-return-values-passed-as-out-parameters"></a>[Out] パラメーターとして渡される OLE 戻り値  
 `retval`COM インターフェイスに戻り値を持ち、 `int` [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 相互運用機能アセンブリメソッドプロトタイプに戻り値と追加の [out] 配列パラメーターを持つメソッドを検索します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]相互運用機能アセンブリメソッドのプロトタイプには COM インターフェイスメソッドよりも1つ多くのパラメーターがあるため、これらのメソッドでは特別な処理が必要であることを明確にする必要があります。  
  
 OLE アクティビティを処理する多くの COM インターフェイスは、OLE ステータスに関する情報を、インターフェイスの戻り値に格納されている呼び出し元のプログラムに送信し `retval` ます。 対応する相互運用機能アセンブリメソッドは、戻り値を使用する代わりに、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [out] 配列パラメーターに格納されている呼び出し元のプログラムに情報を送り返します。  
  
 これらのメソッドのマネージ実装では、[out] パラメーターと同じ型の単一要素配列を作成し、パラメーターに配置する必要があります。 配列要素の値は、適切な COM と同じである必要があり `retval` ます。  
  
 この型のインターフェイスを呼び出すマネージメソッドは、[out] 配列から最初の要素を取得する必要があります。 この要素は、 `retval` 対応する COM インターフェイスからの戻り値として扱うことができます。  
  
## <a name="see-also"></a>参照  
 [相互運用マーシャリング](https://msdn.microsoft.com/a95fdb76-7c0d-409e-a77e-0349b1ea1490)   
 [相互運用マーシャリング](https://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)   
 [相互運用性のトラブルシューティング](https://msdn.microsoft.com/library/b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37)   
 [マネージド VSPackage](../misc/managed-vspackages.md)