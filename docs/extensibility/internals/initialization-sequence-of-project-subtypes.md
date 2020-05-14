---
title: プロジェクトサブタイプの初期化シーケンス |マイクロソフトドキュメント
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
ms.openlocfilehash: 05a3c312f61dd2b2c63c3f38ef8bac2203b326db
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707633"
---
# <a name="initialization-sequence-of-project-subtypes"></a>プロジェクト サブタイプの初期化シーケンス
環境は、基本プロジェクト ファクトリの実装を呼び出すことによって<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>プロジェクトを構築します。 プロジェクト ファイルの拡張子のプロジェクトの種類 GUID リストが空でないと環境が判断したときに、プロジェクト のサブタイプの構築が開始されます。 プロジェクト ファイルの拡張子とプロジェクト GUID は、プロジェクト[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]の[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]種類を指定します。 たとえば、.vbproj 拡張子と {F184B08F-C81C-45F6-A57F-5ABD9991F28F} は[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]プロジェクトを識別します。

## <a name="environments-initialization-of-project-subtypes"></a>環境のプロジェクト サブタイプの初期化
 次の手順では、複数のプロジェクト サブタイプによって集計されたプロジェクト システムの初期化順序を詳しく説明します。

1. 環境は基本プロジェクトの<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>を呼び出し、プロジェクトがプロジェクト ファイルを解析している間に、プロジェクトの種類の集計の GUID`null`リストが . プロジェクトはプロジェクトの直接作成を中止します。

2. プロジェクトは、`QueryService`環境<xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject>のメソッドの実装を使用してプロジェクトのサブタイプを作成するサービス<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>を呼び出します。 このメソッド内では、環境は、プロジェクトの種類 GUID<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>の<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>リスト<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>をウォークしながら、最も外側のプロジェクト サブタイプから始めて、 の実装とメソッドに対して再帰的な関数呼び出しを行います。

     初期化手順の詳細を次に示します。

    1. 環境のメソッドの実装は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>次の関数`HrCreateInnerProj`宣言を使用してメソッドを呼び出します。

         \<>0</CodeContentPlaceHolder>

         この関数が初めて呼び出されたとき、つまり、最も外側のプロジェクトサブタイプに対して、`pOuter`パラメータ`pOwner`とパラメータが渡`null`され、関数は最も外側のプロジェクトサブ`IUnknown`タイプ`pOuter`をに設定します。

    2. 次に、一`HrCreateInnerProj`覧内の 2 番目のプロジェクトの種類の GUID を持つ関数を呼び出します。 この GUID は、集約シーケンスで基本プロジェクトに向かってステップインする 2 番目の内部プロジェクトサブタイプに対応します。

    3. `pOuter`は、最も外側の`IUnknown`プロジェクトサブタイプの を指し示`HrCreateInnerProj`し、 の<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>実装を呼び出し、その<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>後に、 の実装を呼び出します。 メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>では、最も外側`IUnknown`のプロジェクトサブタイプの制御で渡します。 `pOuter` 所有プロジェクト (内部プロジェクトサブタイプ) は、ここで集計プロジェクト オブジェクトを作成する必要があります。 メソッドの<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>実装では、集約される内部プロジェクト`IUnknown`の へのポインターを渡します。 これら 2 つのメソッドは、集計オブジェクトを作成し、実装は、プロジェクトのサブタイプがそれ自体への参照カウントを保持しないように、COM の集計規則に従う必要があります。

    4. `HrCreateInnerProj`の実装を呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>び出します。 このメソッドでは、プロジェクトのサブタイプは初期化作業を行います。 たとえば、ソリューション イベントを に<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>登録できます。

    5. `HrCreateInnerProj`は、リスト内の最後の GUID (基本プロジェクト) に到達するまで再帰的に呼び出されます。 これらの呼び出しごとに、c から d までのステップが繰り返されます。 `pOuter`は、集計の各レベルの最`IUnknown`も外側のプロジェクト サブタイプを指します。

## <a name="example"></a>例

次の例では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A>環境によって実装されるメソッドの概略表現で、プログラムプロセスの詳細を示します。 コードは単なる例です。コンパイルを意図したものではなく、わかりやすくするためにすべてのエラー チェックが削除されました。

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

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
