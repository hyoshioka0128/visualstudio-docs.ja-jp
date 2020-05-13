---
title: プロジェクト オブジェクトの公開 |マイクロソフトドキュメント
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
ms.openlocfilehash: 81446fa582524872b03199ae707f658776787961
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708471"
---
# <a name="expose-project-objects"></a>プロジェクト オブジェクトを公開する

カスタム プロジェクトの種類は、オートメーション インターフェイスを使用してプロジェクトにアクセスできるようにするためにオートメーション オブジェクトを提供できます。 すべてのプロジェクトの種類は、IDE で<xref:EnvDTE.Project>開かれているすべてのプロジェクトのコレクション<xref:EnvDTE.Solution>を含む からアクセスされる標準のオートメーション オブジェクトを提供する必要があります。 プロジェクト内の各項目は、 で<xref:EnvDTE.ProjectItem>`Project.ProjectItems`アクセスされるオブジェクトによって公開される必要があります。 これらの標準オートメーションオブジェクトに加えて、プロジェクト固有のオートメーションオブジェクトを提供することもできます。

または を使用して`DTE.<customObjectName>`ルート DTE オブジェクトから遅延バインディングにアクセスできるカスタム ルート レベルのオートメーション`DTE.GetObject("<customObjectName>")`オブジェクトを作成できます。 たとえば、Visual C++ では *、C++* プロジェクト固有のプロジェクト コレクション VCProjects を`DTE.VCProjects`作成`DTE.GetObject("VCProjects")`します。 また、プロジェクトの種類`Project.Object`に対して一意である、 、最`Project.CodeModel`派生オブジェクト`ProjectItem`を照会できる 、 を作成`ProjectItem.Object`することもできます。 `ProjectItem.FileCodeModel`

プロジェクトでは、プロジェクト固有のカスタム プロジェクト コレクションを公開するのが一般的な規則です。 たとえば、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]または を使用して`DTE.VCProjects`アクセスできる C++ 固有のプロジェクト`DTE.GetObject("VCProjects")`コレクションを作成します。 また、プロジェクトの種類`Project.Object`に対して一意である、 、`Project.CodeModel`その最派生オブジェクト、を公開する`ProjectItem`、 を照会する 、`ProjectItem.Object`を作成することもできます。 `ProjectItem.FileCodeModel`

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>プロジェクトに VSPackage 固有のオブジェクトを提供するには

1. VS パッケージの *.pkgdef*ファイルに適切なキーを追加します。

     たとえば、C++ 言語プロジェクトの *.pkgdef*設定を次に示します。

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. 次の例のように、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>メソッドにコードを実装します。

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

     コード内の`g_wszAutomationProjects`プロジェクト コレクションの名前です。 この`GetAutomationProjects`メソッドは、インターフェイスを実装するオブジェクト`Projects`を作成し、`IDispatch`呼び出し元のオブジェクトへのポインターを返します。

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

     オートメーションオブジェクトの一意の名前を選択します。 名前の競合は予測不能であり、複数のプロジェクトの種類が同じ名前を使用している場合、競合するオブジェクト名が任意にスローされます。 オートメーション オブジェクトの名前には、会社名またはその製品名の一意の側面を含める必要があります。

     カスタム`Projects`コレクション オブジェクトは、プロジェクトオートメーションモデルの残りの部分の便利なエントリポイントです。 プロジェクト オブジェクトには、<xref:EnvDTE.Solution>プロジェクト コレクションからもアクセスできます。 コンシューマーに`Projects`コレクション オブジェクトを提供する適切なコードとレジストリ エントリを作成したら、実装でプロジェクト モデルの残りの標準オブジェクトを提供する必要があります。 詳細については、「[プロジェクトモデリング](../../extensibility/internals/project-modeling.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
