---
title: プロジェクトのサブタイプの初期化シーケンス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c5594d54c188c2f561dd66229e808e48068ba41a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192660"
---
# <a name="initialization-sequence-of-project-subtypes"></a>プロジェクト サブタイプの初期化シーケンス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

環境では、の基本プロジェクトファクトリの実装を呼び出すことによって、プロジェクトを構築し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> ます。 プロジェクトのサブタイプの構造は、プロジェクトファイルの拡張子に対するプロジェクトの種類の GUID リストが空でないと判断したときに開始されます。 プロジェクトファイルの拡張子とプロジェクト GUID は、プロジェクトがプロジェクトの種類であるか、またはプロジェクトであるかを指定し [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] ます。 たとえば、.vbproj 拡張子と {F184B08F-C81C-45F6-A57F-5ABD9991F28F} はプロジェクトを識別します [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 。  
  
## <a name="environments-initialization-of-project-subtypes"></a>環境におけるプロジェクトのサブタイプの初期化  
 次の手順では、複数のプロジェクトサブタイプによって集計されたプロジェクトシステムの初期化シーケンスについて詳しく説明します。  
  
1. 環境は基本プロジェクトのを呼び出し、プロジェクト <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> はそのプロジェクトファイルを解析しますが、[プロジェクトの種類の集計] の一覧ではないことを検出し `null` ます。 プロジェクトはプロジェクトの直接作成を中止します。  
  
2. プロジェクトは、 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> メソッドの環境の実装を使用してプロジェクトのサブタイプを作成するために、サービスでを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> ます。 このメソッド内では、環境によって、の実装に対して再帰的な関数呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> `M:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject(System.Object)` が行わ <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> れます。また、プロジェクトの種類の guid の一覧を調べている間は、最も外側のプロジェクトのサブタイプから開始されます。  
  
    次に、初期化の手順の詳細を示します。  
  
   1. 環境のメソッドの実装は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 次の関数宣言を使用して ' HrCreateInnerProj ' ' ' メソッドを呼び出します。  
  
       ```  
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
           BOOL *pfCancelled  
       )  
       ```  
  
        この関数が初めて呼び出されたとき、つまり最も外側のプロジェクトのサブタイプに対してパラメーターとが渡されると、 `pOuter` `pOwner` `null` 関数は最も外側のプロジェクトのサブタイプ `IUnknown` をに設定し `pOuter` ます。  
  
   2. 次に、環境は、 `HrCreateInnerProj` リスト内の2番目のプロジェクトの種類の GUID を使用して関数を呼び出します。 この GUID は、集計シーケンスの基本プロジェクトにステップインする2番目の内部プロジェクトサブタイプに対応します。  
  
   3. `pOuter`は、 `IUnknown` 最も外側のプロジェクトのサブタイプのをポイントし、の `HrCreateInnerProj` 実装を呼び出した <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 後、の実装を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> ます。 メソッドでは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> `IUnknown` 最も外側のプロジェクトのサブタイプの制御を渡し `pOuter` ます。 所有されているプロジェクト (内部プロジェクトのサブタイプ) は、ここで集計プロジェクトオブジェクトを作成する必要があります。 メソッドの実装では、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 集計される内部プロジェクトのへのポインターを渡し `IUnknown` ます。 これらの2つのメソッドは、集計オブジェクトを作成します。実装では、プロジェクトのサブタイプがそれ自体に参照カウントを保持しないようにするために、COM 集計規則に従う必要があります。  
  
   4. `HrCreateInnerProj` の実装を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> ます。 このメソッドでは、プロジェクトのサブタイプは初期化に使用されます。 たとえば、にソリューションイベントを登録でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> ます。  
  
   5. `HrCreateInnerProj` は、リスト内の最後の GUID (基本プロジェクト) に到達するまで再帰的に呼び出されます。 これらの各呼び出しについて、c から d までの手順が繰り返されます。 `pOuter` は、集計レベルごとに最も外側のプロジェクトサブタイプを指し `IUnknown` ます。  
  
   次の例で <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> は、環境によって実装される、メソッドのおおよその表現でのプログラムプロセスの詳細について説明します。 コードはほんの一例です。これはコンパイルするためのものではなく、わかりやすくするためにすべてのエラーチェックが削除されました。  
  
## <a name="example"></a>例  
  
### <a name="code"></a>コード  
  
```  
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
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Flavor>   
 [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
