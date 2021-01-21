---
title: プロジェクトのサブタイプの初期化シーケンス |Microsoft Docs
description: 複数のプロジェクトサブタイプによって集計されたプロジェクトシステムの Visual Studio 環境での初期化シーケンスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ea784eae808cbab3a5991651961d3b150b641c04
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98204710"
---
# <a name="initialization-sequence-of-project-subtypes"></a>プロジェクト サブタイプの初期化シーケンス
環境では、の基本プロジェクトファクトリの実装を呼び出すことによって、プロジェクトを構築し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> ます。 プロジェクトのサブタイプの構造は、プロジェクトファイルの拡張子に対するプロジェクトの種類の GUID リストが空でないと判断したときに開始されます。 プロジェクトファイルの拡張子とプロジェクト GUID は、プロジェクトがプロジェクトの種類であるか、またはプロジェクトであるかを指定し [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] ます。 たとえば、.vbproj 拡張子と {F184B08F-C81C-45F6-A57F-5ABD9991F28F} はプロジェクトを識別します [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。

## <a name="environments-initialization-of-project-subtypes"></a>環境におけるプロジェクトのサブタイプの初期化
 次の手順では、複数のプロジェクトサブタイプによって集計されたプロジェクトシステムの初期化シーケンスについて詳しく説明します。

1. 環境は基本プロジェクトのを呼び出し、プロジェクト <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> はそのプロジェクトファイルを解析しますが、[プロジェクトの種類の集計] の一覧ではないことを検出し `null` ます。 プロジェクトはプロジェクトの直接作成を中止します。

2. プロジェクトは、 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> メソッドの環境の実装を使用してプロジェクトのサブタイプを作成するために、サービスでを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> ます。 このメソッド内では、環境によって、の実装に対して再帰的な関数呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> が行わ <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> れます。また、プロジェクトの種類の guid の一覧を調べている間は、最も外側のプロジェクトのサブタイプから開始されます。

     次に、初期化の手順の詳細を示します。

    1. 環境のメソッドの実装は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> `HrCreateInnerProj` 次の関数宣言を使用してメソッドを呼び出します。

         \<CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         この関数が初めて呼び出されたとき、つまり最も外側のプロジェクトのサブタイプに対してパラメーターとが渡されると、 `pOuter` `pOwner` `null` 関数は最も外側のプロジェクトのサブタイプ `IUnknown` をに設定し `pOuter` ます。

    2. 次に、環境は、 `HrCreateInnerProj` リスト内の2番目のプロジェクトの種類の GUID を使用して関数を呼び出します。 この GUID は、集計シーケンスの基本プロジェクトにステップインする2番目の内部プロジェクトサブタイプに対応します。

    3. `pOuter`は、 `IUnknown` 最も外側のプロジェクトのサブタイプのをポイントし、の `HrCreateInnerProj` 実装を呼び出した <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 後、の実装を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> ます。 メソッドでは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> `IUnknown` 最も外側のプロジェクトのサブタイプの制御を渡し `pOuter` ます。 所有されているプロジェクト (内部プロジェクトのサブタイプ) は、ここで集計プロジェクトオブジェクトを作成する必要があります。 メソッドの実装では、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 集計される内部プロジェクトのへのポインターを渡し `IUnknown` ます。 これらの2つのメソッドは、集計オブジェクトを作成します。実装では、プロジェクトのサブタイプがそれ自体に参照カウントを保持しないようにするために、COM 集計規則に従う必要があります。

    4. `HrCreateInnerProj` の実装を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> ます。 このメソッドでは、プロジェクトのサブタイプは初期化に使用されます。 たとえば、にソリューションイベントを登録でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> ます。

    5. `HrCreateInnerProj` は、リスト内の最後の GUID (基本プロジェクト) に到達するまで再帰的に呼び出されます。 これらの各呼び出しについて、c から d までの手順が繰り返されます。 `pOuter` は、集計レベルごとに最も外側のプロジェクトサブタイプを指し `IUnknown` ます。

## <a name="example"></a>例

次の例で <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> は、環境によって実装される、メソッドのおおよその表現でのプログラムプロセスの詳細について説明します。 コードはほんの一例です。これはコンパイルするためのものではなく、わかりやすくするためにすべてのエラーチェックが削除されました。

```cpp
HRESULT CreateAggregateProject
(
    LPCOLESTR lpstrGuids,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    REFIID iidProject,
    void **ppvProject)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpunkProj;
    CComPtr<IVsAggregatableProject> srpAggProject;
    CComBSTR bstrGuids = lpstrGuids;
    BOOL fCanceled = FALSE;
    *ppvProject = NULL;

    HrCreateInnerProj(
         bstrGuids, NULL, NULL, pszFilename, pszLocation,
         pszName, grfCreateFlags, &srpunkProj, &fCanceled);
    srpunkProj->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggProject));
    srpAggProject->OnAggregationComplete();
    srpunkProj->QueryInterface(iidProject, ppvProject);
}

HRESULT HrCreateInnerProj
(
    WCHAR *pwszGuids,
    IUnknown *pOuter,
    IVsAggregatableProject *pOwner,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    IUnknown **ppInner,
    BOOL *pfCanceled
)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpInner;
    CComPtr<IVsAggregatableProject> srpAggInner;
    CComPtr<IVsProjectFactory> srpProjectFactory;
    CComPtr<IVsAggregatableProjectFactory> srpAggPF;
    GUID guid = GUID_NULL;
    WCHAR *pwszNextGuids = wcschr(pwszGuids, L';');
    WCHAR wszText[_MAX_PATH+150] = L"";

    if (pwszNextGuids)
    {
        *pwszNextGuids++ = 0;
    }

    CLSIDFromString(pwszGuids, &guid);
    GetProjectTypeMgr()->HrGetProjectFactoryOfGuid(
        guid, &srpProjectFactory);
    srpProjectFactory->QueryInterface(
        IID_IVsAggregatableProjectFactory,
        (void **)&srpAggPF);
    srpAggPF->PreCreateForOuter(pOuter, &srpInner);
    srpInner->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggInner);

    if (pOwner)
    {
        IfFailGo(pOwner->SetInnerProject(srpInner));
    }

    if (pwszNextGuids)
    {
        CComPtr<IUnknown> srpNextInner;
        HrCreateInnerProj(
            pwszNextGuids, pOuter ? pOuter : srpInner,
            srpAggInner, pszFilename, pszLocation, pszName,
            grfCreateFlags, &srpNextInner, pfCanceled);
    }

    return srpAggInner->InitializeForOuter(
        pszFilename, pszLocation, pszName, grfCreateFlags,
        IID_IUnknown, (void **)ppInner, pfCanceled);
}
```

## <a name="see-also"></a>こちらもご覧ください

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
