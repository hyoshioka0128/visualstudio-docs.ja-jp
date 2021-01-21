---
title: プロジェクトオブジェクトの公開 |Microsoft Docs
description: オートメーションインターフェイスを使用してプロジェクトへのアクセスを許可するオートメーションオブジェクトを提供することによって、Visual Studio でカスタムプロジェクトの種類のオブジェクトを公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project objects, exposing
- extensibility, project objects
ms.assetid: 5bb24967-434a-4ef4-87a0-2f3250c9e22d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d93b1bf414a9e58f8311a1f1d7066a789ef8c6b6
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96479512"
---
# <a name="expose-project-objects"></a>プロジェクトオブジェクトの公開

カスタムプロジェクトの種類でオートメーションオブジェクトを提供して、オートメーションインターフェイスを使用してプロジェクトにアクセスできるようにすることができます。 すべてのプロジェクトの種類は <xref:EnvDTE.Project> 、からアクセスされる標準のオートメーションオブジェクトを提供することを想定しています。このオブジェクトには <xref:EnvDTE.Solution> 、IDE で開いているすべてのプロジェクトのコレクションが含まれています。 プロジェクト内の各項目は、でアクセスされるオブジェクトによって公開されることが想定されてい <xref:EnvDTE.ProjectItem> `Project.ProjectItems` ます。 これらの標準オートメーションオブジェクトに加えて、プロジェクトはプロジェクト固有のオートメーションオブジェクトを提供するように選択できます。

またはを使用してルート DTE オブジェクトから遅延バインディングにアクセスできる、カスタムルートレベルのオートメーションオブジェクトを作成でき `DTE.<customObjectName>` `DTE.GetObject("<customObjectName>")` ます。 たとえば、Visual C++ は、またはを使用してアクセスできる *Vcprojects* という C++ プロジェクト固有のプロジェクトコレクションを作成し `DTE.VCProjects` `DTE.GetObject("VCProjects")` ます。 を作成することもできます `Project.Object` 。これは、プロジェクトの種類に対して一意であり、 `Project.CodeModel` 最も派生したオブジェクトに対してクエリを実行できる、およびを公開するを作成し `ProjectItem` `ProjectItem.Object` `ProjectItem.FileCodeModel` ます。

プロジェクトは、プロジェクト固有のカスタムプロジェクトコレクションを公開するための一般的な規則です。 たとえば、 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] は、またはを使用してアクセスできる C++ 特定のプロジェクトコレクションを作成し `DTE.VCProjects` `DTE.GetObject("VCProjects")` ます。 また、 `Project.Object` プロジェクトの種類に対して一意のを作成することもできます。これは、最も派生したオブジェクト、、を公開する、およびを照会することができ `Project.CodeModel` `ProjectItem` `ProjectItem.Object` `ProjectItem.FileCodeModel` ます。

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>プロジェクトの VSPackage 固有のオブジェクトを投稿するには

1. VSPackage の *pkgdef* ファイルに適切なキーを追加します。

     たとえば、C++ 言語プロジェクトの *pkgdef* 設定を次に示します。

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. 次の例のように、メソッドにコードを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> ます。

    ```cpp
    STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
    {
    ExpectedPtrRet(pszPropName);
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

        if (m_fZombie)
            return E_UNEXPECTED;

        if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        {
            return GetAutomationProjects(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        return E_INVALIDARG;
    }
    ```

     コードでは、 `g_wszAutomationProjects` はプロジェクトコレクションの名前です。 メソッドは、 `GetAutomationProjects` `Projects` 次のコード例に示すように、インターフェイスを実装し、 `IDispatch` 呼び出し元のオブジェクトへのポインターを返すオブジェクトを作成します。

    ```cpp
    HRESULT CVsPackage::GetAutomationProjects(/* [out] */ IDispatch ** ppIDispatch)
    {
        ExpectedPtrRet(ppIDispatch);
        *ppIDispatch = NULL;

        if (!m_srpAutomationProjects)
        {
            HRESULT hr = CACProjects::CreateInstance(&m_srpAutomationProjects);
            IfFailRet(hr);
            ExpectedExprRet(m_srpAutomationProjects != NULL);
        }
        return m_srpAutomationProjects.CopyTo(ppIDispatch);
    }
    ```

     オートメーションオブジェクトの一意の名前を選択します。 名前の競合は予測できません。また、複数のプロジェクトの種類で同じ名前を使用している場合は、競合するオブジェクト名が任意にスローされます。 オートメーションオブジェクトの名前に、会社名または製品名の固有の側面を含める必要があります。

     カスタム `Projects` コレクションオブジェクトは、プロジェクトオートメーションモデルの残りの部分の便利なエントリポイントです。 プロジェクトオブジェクトは、プロジェクトコレクションからアクセスすることもでき <xref:EnvDTE.Solution> ます。 コンシューマーにコレクションオブジェクトを提供する適切なコードとレジストリエントリを作成したら `Projects` 、その実装でプロジェクトモデルの残りの標準オブジェクトを提供する必要があります。 詳細については、「 [プロジェクトモデリング](../../extensibility/internals/project-modeling.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
