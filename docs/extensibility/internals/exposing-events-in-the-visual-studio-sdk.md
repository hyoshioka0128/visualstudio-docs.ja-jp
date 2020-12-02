---
title: Visual Studio SDK でのイベントの公開 |Microsoft Docs
description: プロジェクトおよびプロジェクト項目のイベントを公開する Visual Studio SDK のメソッドとレジストリエントリについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d5eec842f989497fda618482916154aabdcdd406
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96480539"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>Visual Studio SDK でイベントを公開する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オートメーションを使用してイベントのソースを作成できます。 プロジェクトとプロジェクトアイテムのイベントをソースにすることをお勧めします。

 イベントは、オートメーションコンシューマーによって <xref:EnvDTE.DTEClass.Events%2A> オブジェクトまたは (など) から取得され <xref:EnvDTE.DTEClass.GetObject%2A> `GetObject("EventObjectName")` ます。 環境は、 `IDispatch::Invoke` またはフラグを使用してを呼び出し、 `DISPATCH_METHOD` `DISPATCH_PROPERTYGET` イベントを返します。

 次のプロセスでは、VSPackage 固有のイベントがどのように返されるかを説明します。

1. 環境が起動します。

2. このメソッドは、すべての Vspackage の **Automation**、 **AutomationEvents**、および **automationproperties.automationid** キーの下にあるすべての値名をレジストリから読み取り、それらの名前をテーブルに格納します。

3. オートメーションコンシューマーは、この例では、 `DTE.Events.AutomationProjectsEvents` またはを呼び出し `DTE.Events.AutomationProjectItemsEvents` ます。

4. 環境では、テーブル内の文字列パラメーターを検索し、対応する VSPackage を読み込みます。

5. 環境は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 呼び出しで渡される名前 (この例で `AutomationProjectsEvents` は、または) を使用してメソッドを呼び出し `AutomationProjectItemsEvents` ます。

6. VSPackage は、やなどのメソッドを含むルートオブジェクトを作成し、 `get_AutomationProjectsEvents` `get_AutomationProjectItemEvents` オブジェクトへの IDispatch ポインターを返します。

7. 環境は、オートメーション呼び出しに渡された名前に基づいて適切なメソッドを呼び出します。

8. メソッドは、 `get_` インターフェイスとインターフェイスの両方を実装する別の IDispatch ベースのイベントオブジェクト `IConnectionPointContainer` を作成し、 `IConnectionPoint` オブジェクトにを返し `IDispatchpointer` ます。

   オートメーションを使用してイベントを公開するには、に応答 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> し、レジストリに追加する文字列を監視する必要があります。 基本的なプロジェクトのサンプルでは、文字列は *BscProjectsEvents* と *BscProjectItemsEvents* です。

## <a name="registry-entries-from-the-basic-project-sample"></a>基本的なプロジェクトのサンプルのレジストリエントリ
 ここでは、レジストリにオートメーションイベントの値を追加する方法について説明します。

 **[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Packages\\<PkgGUID \> \AutomationEvents]**

 **AutomationProjectEvents** = オブジェクトを返し `AutomationProjectEvents` ます。

 **AutomationProjectItemEvents** = オブジェクトを返し `AutomationProjectItemsEvents` ます。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|既定値 (@)|REG_SZ|未使用|未使用。 データフィールドはドキュメントに使用できます。|
|*AutomationProjectsEvents*|REG_SZ|イベントオブジェクトの名前。|キー名のみが関連しています。 データフィールドはドキュメントに使用できます。<br /><br /> この例は、基本的なプロジェクトサンプルから取得したものです。|
|*AutomationProjectItemEvents*|REG_SZ|イベントオブジェクトの名前|キー名のみが関連しています。 データフィールドはドキュメントに使用できます。<br /><br /> この例は、基本的なプロジェクトサンプルから取得したものです。|

 いずれかのイベントオブジェクトがオートメーションコンシューマーによって要求された場合は、VSPackage がサポートする任意のイベントのメソッドを含むルートオブジェクトを作成します。 環境は、 `get_` このオブジェクトの適切なメソッドを呼び出します。 たとえば、 `DTE.Events.AutomationProjectsEvents` が呼び出されると、 `get_AutomationProjectsEvents` ルートオブジェクトのメソッドが呼び出されます。

 ![Visual Studio プロジェクトのイベント](../../extensibility/internals/media/projectevents.gif "ProjectEvents") イベントのオートメーションモデル

 クラスは、 `CProjectEventsContainer` *BscProjectsEvents* のソースオブジェクトを表し、 `CProjectItemsEventsContainer` *BscProjectItemsEvents* のソースオブジェクトを表します。

 ほとんどのイベントオブジェクトはフィルターオブジェクトを受け取るため、ほとんどの場合、すべてのイベント要求に対して新しいオブジェクトを返す必要があります。 イベントを発生させたら、このフィルターをオンにして、イベントハンドラーが呼び出されていることを確認します。

 *AutomationEvents* と *AutomationEvents* には、次の表に示すクラスの宣言と実装が含まれています。

|クラス|説明|
|-----------|-----------------|
|`CAutomationEvents`|オブジェクトから取得されたイベントルートオブジェクトを実装し `DTE.Events` ます。|
|`CProjectsEventsContainer` および `CProjectItemsEventsContainer`|対応するイベントを発生させるイベントソースオブジェクトを実装します。|

 次のコード例は、イベントオブジェクトの要求に応答する方法を示しています。

```cpp
STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
{
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

    if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        //Is the requested name our Projects object?
    {
        return GetAutomationProjects(ppIDispatch);
        // Gets our Projects object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        //Is the requested name our ProjectsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectEvents object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)  //Is the requested name our ProjectsItemsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectItemsEvents object.
    }
    return E_INVALIDARG;
}
```

 上記のコードで `g_wszAutomationProjects` は、はプロジェクトコレクション (*figprojects*)、 `g_wszAutomationProjectsEvents` (*FigProjectsEvents*)、 `g_wszAutomationProjectItemsEvents` (*FigProjectItemEvents*) は、VSPackage 実装から供給されるプロジェクトイベントとプロジェクト項目イベントの名前です。

 イベントオブジェクトは、同じ中央の場所 (オブジェクト) から取得され `DTE.Events` ます。 これにより、すべてのイベントオブジェクトがグループ化され、エンドユーザーが特定のイベントを検索するためにオブジェクトモデル全体を参照する必要がなくなります。 これにより、システム全体のイベント用に独自のコードを実装する必要がなく、特定の VSPackage オブジェクトを提供することもできます。 ただし、エンドユーザーがインターフェイスのイベントを検索する必要がある場合、その `ProjectItem` イベントオブジェクトの取得元からはすぐにはわかりません。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
