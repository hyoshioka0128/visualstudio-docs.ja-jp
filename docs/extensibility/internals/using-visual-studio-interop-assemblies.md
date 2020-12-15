---
title: Visual Studio 相互運用機能アセンブリの使用 |Microsoft Docs
description: Visual Studio の相互運用機能アセンブリが、Visual Studio の機能拡張を提供する COM インターフェイスにアクセスできるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c52dd2cf8c76cdef9be5080950d5f1b9e621e70
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487661"
---
# <a name="using-visual-studio-interop-assemblies"></a>Visual Studio 相互運用機能アセンブリの使用
Visual Studio 相互運用機能アセンブリを使用すると、マネージアプリケーションは Visual Studio の拡張機能を提供する COM インターフェイスにアクセスできます。 ストレート COM インターフェイスとその相互運用バージョンにはいくつかの違いがあります。 たとえば、Hresult は通常 int 値として表され、例外と同様に処理する必要があり、パラメーター (特に出力パラメーター) は異なる方法で処理する必要があります。

## <a name="handling-hresults-returned-to-managed-code-from-com"></a>COM からマネージド コードに返される HRESULT の処理
 マネージド コードから COM インターフェイスを呼び出す場合は、HRESULT 値を確認し、必要な場合に例外をスローします。 渡された HRESULT の値に応じて、<xref:Microsoft.VisualStudio.ErrorHandler> クラスには COM 例外をスローする <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> メソッドが含まれます。

 既定では、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> は、0 より小さい値を持つ HRESULT を渡されるたびに例外をスローします。 このような HRESULT が許容される値であり、例外をスローする必要がない場合は、値のテスト後に追加 HRESULT の値を <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> に渡す必要があります。 テスト対象の HRESULT が、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> に明示的に渡される HRESULT 値と一致する場合、例外はスローされません。

> [!NOTE]
> クラスには、、などの <xref:Microsoft.VisualStudio.VSConstants> 一般的な hresult の定数、および <xref:Microsoft.VisualStudio.VSConstants.S_OK> <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] hresult (やなど) が含まれてい <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT> ます。 また、<xref:Microsoft.VisualStudio.VSConstants> には、COM の SUCCEEDED および FAILED マクロに対応する <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> および <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> メソッドが用意されています。

 たとえば、<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> が許容可能な戻り値であり、ゼロ未満の他の HRESULT がエラーを表す次の関数呼び出しがあるとします。

 [!code-vb[VSSDKHRESULTInformation#1](../../extensibility/internals/codesnippet/VisualBasic/using-visual-studio-interop-assemblies_1.vb)]
 [!code-csharp[VSSDKHRESULTInformation#1](../../extensibility/internals/codesnippet/CSharp/using-visual-studio-interop-assemblies_1.cs)]

 許容可能な戻り値が複数ある場合は、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> への呼び出しの一覧にのみ追加の HRESULT 値を追加することができます。

 [!code-vb[VSSDKHRESULTInformation#2](../../extensibility/internals/codesnippet/VisualBasic/using-visual-studio-interop-assemblies_2.vb)]
 [!code-csharp[VSSDKHRESULTInformation#2](../../extensibility/internals/codesnippet/CSharp/using-visual-studio-interop-assemblies_2.cs)]

## <a name="returning-hresults-to-com-from-managed-code"></a>マネージド コードから COM に HRESULT を返す
 例外が発生しない場合、マネージド コードは呼び出し元の COM 関数に <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返します。 COM 相互運用では、マネージド コードで厳密に型指定される一般的な例外がサポートされます。 たとえば、受け入れられない `null` 引数を受け取るメソッドは、<xref:System.ArgumentNullException> をスローします。

 スローする例外が不明であり、COM に戻す HRESULT がわかっている場合は、<xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> メソッドを使用して、適切な例外をスローすることができます。 これは、<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> などの非標準のエラーでも機能します。 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> では、渡された HRESULT を厳密に型指定された例外にマップすることを試みます。 できない場合は、代わりに一般的な COM 例外をスローします。 最終的な結果では、マネージド コードから <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> に渡す HRESULT が呼び出し元の COM 関数に返されます。

> [!NOTE]
> 例外によって、パフォーマンスが低下します。例外は、異常なプログラムの条件を示すことを目的としています。 頻繁に発生する条件は、スローされた例外ではなく、インラインで処理をする必要があります。

## <a name="iunknown-parameters-passed-as-type-void"></a>型 void * * として渡された IUnknown パラメーター
 COM インターフェイスで型として定義されている `void **` が、 `[``iid_is``]` [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリメソッドプロトタイプでとして定義されている [out] パラメーターを検索します。

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

## <a name="optional-out-parameters"></a>省略可能な [out] パラメーター
 COM インターフェイスで [out] データ型 (、など) として定義されているパラメーターを検索し `int` `object` ますが、これは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリメソッドプロトタイプで同じデータ型の配列として定義されています。

 などの一部の COM インターフェイスで <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> は、[out] パラメーターをオプションとして扱います。 オブジェクトが不要な場合、これらの COM インターフェイスは、 `null` [out] オブジェクトを作成するのではなく、そのパラメーターの値としてポインターを返します。 これは仕様です。 これらのインターフェイスでは、 `null` ポインターは VSPackage の正しい動作の一部と見なされ、エラーは返されません。

 CLR では [out] パラメーターの値をにすることが許可されていないため `null` 、これらのインターフェイスのデザインされた動作の一部をマネージコード内で直接使用することはできません。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]影響を受けるインターフェイスの相互運用機能アセンブリメソッドは、関連するパラメーターを配列として定義することで問題を回避します。これは、CLR が配列を渡すことができるため `null` です。

 これらのメソッドのマネージ実装は、 `null` 返されるものがない場合に、配列をパラメーターに配置する必要があります。 それ以外の場合は、正しい型の1つの要素から成る配列を作成し、戻り値を配列に格納します。

 省略可能な [out] パラメーターを使用してインターフェイスから情報を受け取るマネージメソッドは、パラメーターを配列として受け取ります。 配列の最初の要素の値を確認するだけです。 それ以外の場合は `null` 、最初の要素を元のパラメーターとして扱います。

## <a name="passing-constants-in-pointer-parameters"></a>ポインターパラメーターでの定数の引き渡し
 COM インターフェイスで [in] ポインターとして定義されているが、 <xref:System.IntPtr> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリのメソッドプロトタイプで型として定義されているパラメーターを探します。

 同様の問題は、COM インターフェイスがオブジェクトポインターではなく、0、-1、または-2 などの特別な値を渡した場合にも発生します。 とは異なり [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 、CLR では、定数をオブジェクトとしてキャストすることはできません。 代わりに、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリがパラメーターを型として定義し <xref:System.IntPtr> ます。

 これらのメソッドのマネージ実装では、 <xref:System.IntPtr> クラスにコンストラクターとコンストラクターの両方が含まれており、必要に応じ `int` `void *` <xref:System.IntPtr> てオブジェクトまたは整数定数からが作成されるという事実を活用する必要があります。

 この型のパラメーターを受け取るマネージメソッドでは、 <xref:System.IntPtr> 型変換演算子を使用して結果を処理する必要があり <xref:System.IntPtr> ます。 まず <xref:System.IntPtr> をに変換 `int` し、関連する整数定数に対してテストします。 一致する値がない場合は、必要な型のオブジェクトに変換して続行します。

 この例については、「」および「」を参照してください <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A> 。

## <a name="ole-return-values-passed-as-out-parameters"></a>[Out] パラメーターとして渡される OLE 戻り値
 `retval`COM インターフェイスに戻り値を持ち、 `int` [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリメソッドプロトタイプに戻り値と追加の [out] 配列パラメーターを持つメソッドを検索します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]相互運用機能アセンブリメソッドのプロトタイプには COM インターフェイスメソッドよりも1つ多くのパラメーターがあるため、これらのメソッドでは特別な処理が必要であることを明確にする必要があります。

 OLE アクティビティを処理する多くの COM インターフェイスは、OLE ステータスに関する情報を、インターフェイスの戻り値に格納されている呼び出し元のプログラムに送信し `retval` ます。 対応する相互運用機能アセンブリメソッドは、戻り値を使用する代わりに、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [out] 配列パラメーターに格納されている呼び出し元のプログラムに情報を送り返します。

 これらのメソッドのマネージ実装では、[out] パラメーターと同じ型の単一要素配列を作成し、パラメーターに配置する必要があります。 配列要素の値は、適切な COM と同じである必要があり `retval` ます。

 この型のインターフェイスを呼び出すマネージメソッドは、[out] 配列から最初の要素を取得する必要があります。 この要素は、 `retval` 対応する COM インターフェイスからの戻り値として扱うことができます。

## <a name="see-also"></a>関連項目
- [アンマネージ コードとの相互運用](/dotnet/framework/interop/index)
