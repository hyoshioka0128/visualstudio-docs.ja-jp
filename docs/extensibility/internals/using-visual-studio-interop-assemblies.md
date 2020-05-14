---
title: ビジュアル スタジオ相互運用機能アセンブリの使用 |マイクロソフトドキュメント
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
ms.openlocfilehash: 5926b2cce217565c889c7ef2eeef877691101ed6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704133"
---
# <a name="using-visual-studio-interop-assemblies"></a>Visual Studio 相互運用機能アセンブリの使用
Visual Studio 相互運用機能アセンブリを使用すると、マネージ アプリケーションから、Visual Studio の機能拡張を提供する COM インターフェイスにアクセスできます。 ストレート COM インターフェイスとそれらの相互運用バージョンには、いくつかの違いがあります。 例えば、HRESULT は一般に int 値として表され、例外と同じ方法で処理する必要があり、パラメーター (特にアウト・パラメーター) は異なる方法で扱われます。

## <a name="handling-hresults-returned-to-managed-code-from-com"></a>COM からマネージド コードに返される HRESULT の処理
 マネージド コードから COM インターフェイスを呼び出す場合は、HRESULT 値を確認し、必要な場合に例外をスローします。 渡された HRESULT の値に応じて、<xref:Microsoft.VisualStudio.ErrorHandler> クラスには COM 例外をスローする <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> メソッドが含まれます。

 既定では、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> は、0 より小さい値を持つ HRESULT を渡されるたびに例外をスローします。 このような HRESULT が許容される値であり、例外をスローする必要がない場合は、値のテスト後に追加 HRESULT の値を <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> に渡す必要があります。 テスト対象の HRESULT が、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> に明示的に渡される HRESULT 値と一致する場合、例外はスローされません。

> [!NOTE]
> この<xref:Microsoft.VisualStudio.VSConstants>クラスには、共通の HRESULTS<xref:Microsoft.VisualStudio.VSConstants.S_OK>の定数が含<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>まれています[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA><xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>。 また、<xref:Microsoft.VisualStudio.VSConstants> には、COM の SUCCEEDED および FAILED マクロに対応する <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> および <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> メソッドが用意されています。

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

## <a name="iunknown-parameters-passed-as-type-void"></a>IUnknown パラメーターは型 void** として渡されます**
 COM インターフェイスで型`void **`として定義されているが、相互運用アセンブリ メソッドのプロトタイプで定義`[``iid_is``]`されている [out][!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]パラメーターを探します。

 場合によっては、COM インターフェイスがオブジェクト`IUnknown`を生成し、そのオブジェクトを型として渡す場合`void **`があります。 これらのインターフェイスは、変数が IDL で [out] として定義されている場合、`IUnknown`オブジェクトがメソッドで参照カウントされるため、特`AddRef`に重要です。 オブジェクトが正しく処理されない場合、メモリ リークが発生します。

> [!NOTE]
> COM`IUnknown`インターフェイスによって作成され、変数 [out] に返されたオブジェクトは、明示的に解放されない場合、メモリ リークを発生させます。

 このようなオブジェクトを処理するマネージ メソッド<xref:System.IntPtr>は、`IUnknown`オブジェクトへのポインターとして扱い、オブジェクト<xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A>を取得するメソッドを呼び出す必要があります。 呼び出し元は、適切な型に戻り値をキャストする必要があります。 オブジェクトが不要になったら、オブジェクトを解放するために<xref:System.Runtime.InteropServices.Marshal.Release%2A>呼び出します。

 メソッドを呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>オブジェクトを正しく処理`IUnknown`する例を次に示します。

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
> 次のメソッドは、オブジェクト`IUnknown`ポインタを type<xref:System.IntPtr>として渡すことを知っています。 このセクションで説明されているように、それらを処理します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>

## <a name="optional-out-parameters"></a>オプションの [out] パラメータ
 COM インターフェイスで [out] データ型 (`int`、`object`など) として定義されているが、相互運用機能アセンブリ メソッド プロトタイプで同じデータ型の配列として定義[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]されているパラメーターを探します。

 などの<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>一部の COM インターフェイスでは、[out] パラメータをオプションとして扱います。 オブジェクトが必要ない場合、これらの COM インターフェイスは`null`[out] オブジェクトを作成する代わりに、そのパラメータの値としてポインタを返します。 これは仕様です。 これらのインターフェイスでは、`null`ポインターは VSPackage の正しい動作の一部として想定され、エラーは返されません。

 CLR では [out] パラメーターの値を使用できないため`null`、これらのインターフェイスの設計された動作の一部は、マネージ コード内で直接使用できません。 CLR[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では`null`配列の受け渡しが許可されているため、影響を受けるインターフェイスの相互運用機能アセンブリ メソッドは、関連するパラメーターを配列として定義することで問題を回避します。

 これらのメソッドのマネージ実装では、返される`null`要素がない場合に、配列をパラメーターに配置する必要があります。 それ以外の場合は、正しい型の 1 つの要素配列を作成し、配列に戻り値を格納します。

 オプションの [out] パラメーターを持つインターフェイスから情報を受け取るマネージ メソッドは、パラメーターを配列として受け取ります。 配列の最初の要素の値を調べるだけです。 がなされていない`null`場合は、最初の要素を元のパラメータとして扱います。

## <a name="passing-constants-in-pointer-parameters"></a>ポインター パラメーターでの定数の引き渡し
 COM インターフェイスで [in] ポインターとして定義されているが、相互運用機能アセンブリ メソッドプロトタイプで<xref:System.IntPtr>型として定義されている[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]パラメーターを探します。

 同様の問題は、COM インターフェイスがオブジェクト ポインタではなく、0、-1、-2 などの特別な値を渡すときに発生します。 と[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]は異なり、CLR では、定数をオブジェクトとしてキャストすることはできません。 代わりに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]相互運用アセンブリはパラメーターを<xref:System.IntPtr>型として定義します。

 これらのメソッドのマネージ<xref:System.IntPtr>実装では、クラスに両方のコンストラクタと`int``void *`コンストラクタが含まれ、オブジェクトまたは整数定数<xref:System.IntPtr>から作成される必要があります。

 この型のパラメーター<xref:System.IntPtr>を受け取るマネージ<xref:System.IntPtr>メソッドは、結果を処理するために型変換演算子を使用する必要があります。 まずに<xref:System.IntPtr>を`int`変換し、関連する整数定数に対してテストします。 一致する値がない場合は、必要な型のオブジェクトに変換して続行します。

 この例については、 および<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>を参照してください。

## <a name="ole-return-values-passed-as-out-parameters"></a>[out] パラメータとして渡された OLE 戻り値
 COM インターフェイスで戻り`retval`値を持つメソッドを検索しますが、相互運用`int`機能アセンブリ メソッドのプロトタイプに戻り値と追加[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の [out] 配列パラメーターがあるメソッド。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]相互運用機能アセンブリ メソッドのプロトタイプには COM インターフェイス メソッドより 1 つ多くのパラメーターがあるため、これらのメソッドには特別な処理が必要であることは明らかです。

 OLE アクティビティを扱う多くの COM インターフェイスは、インターフェイスの戻り値に格納`retval`されている呼び出し元のプログラムに、OLE ステータスに関する情報を返します。 戻り値を使用する代わりに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]対応する相互運用アセンブリ メソッドは、情報を [out] 配列パラメーターに格納された呼び出し元のプログラムに返送します。

 これらのメソッドのマネージ実装では、[out] パラメーターと同じ型の単一要素配列を作成し、パラメーターに配置する必要があります。 配列要素の値は、適切な COM`retval`と同じである必要があります。

 この型のインターフェイスを呼び出すマネージ メソッドは、最初の要素を [out] 配列から引き出す必要があります。 この要素は、対応する COM インターフェイス`retval`からの戻り値として扱うことができます。

## <a name="see-also"></a>関連項目
- [アンマネージ コードとの相互運用](/dotnet/framework/interop/index)
