---
title: イベントを公開するマイクロソフトドキュメント
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
ms.openlocfilehash: 48f1e0ea0dcd07bbc26fc89d5c61a6a5941d4727
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708484"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>イベントを公開する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、オートメーションを使用してイベントをソースすることができます。 プロジェクトとプロジェクト項目のイベントをソースにすることをお勧めします。

 イベントは、<xref:EnvDTE.DTEClass.Events%2A>オートメーション コンシューマによってオブジェクトから取得されます<xref:EnvDTE.DTEClass.GetObject%2A>( など)。 `GetObject("EventObjectName")` 環境は、`IDispatch::Invoke`または`DISPATCH_PROPERTYGET``DISPATCH_METHOD`フラグを使用してイベントを返すことによって呼び出します。

 次のプロセスでは、VSPackage 固有のイベントが返される方法について説明します。

1. 環境が開始されます。

2. レジストリからすべての値名を読み取る、**オートメーション**、**オートメーション イベント**、およびオートメーション**プロパティ**のすべての VSPackages キー、およびテーブルに格納します。

3. この例では、オートメーション コンシューマ呼び`DTE.Events.AutomationProjectsEvents`出`DTE.Events.AutomationProjectItemsEvents`し、 または .

4. 環境は、テーブル内の文字列パラメーターを検索し、対応する VSPackage を読み込みます。

5. 環境は、呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>び出しで渡された名前を使用してメソッドを呼び出します。この例では、 `AutomationProjectsEvents` `AutomationProjectItemsEvents`または を使用します。

6. などのメソッド`get_AutomationProjectsEvents``get_AutomationProjectItemEvents`を持つ、および、オブジェクトへの IDispatch ポインターを返すルート オブジェクトを作成します。

7. 環境は、オートメーション呼び出しに渡された名前に基づいて適切なメソッドを呼び出します。

8. この`get_`メソッドは、インターフェイスとインターフェイスの両方を実装し、オブジェクトに`IConnectionPointContainer`a`IConnectionPoint`を`IDispatchpointer`返す、別の IDispatch ベースのイベント オブジェクトを作成します。

   オートメーションを使用してイベントを公開するには、レジストリに追加<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>する文字列に応答して監視する必要があります。 基本プロジェクトのサンプルでは、文字列は*Bsc プロジェクト イベント*と*Bsc プロジェクトイベントです*。

## <a name="registry-entries-from-the-basic-project-sample"></a>基本プロジェクトサンプルからのレジストリ エントリ
 このセクションでは、オートメーション イベント値をレジストリに追加する場所を示します。

 **[HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\8.0\パッケージ\\<PkgGUID\>\オートメーションイベント]**

 **オブジェクトを**返します`AutomationProjectEvents`。

 **オブジェクトを**返します`AutomationProjectItemsEvents`。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|デフォルト (@)|REG_SZ|未使用|未使用。 データ フィールドを使用してドキュメントを作成できます。|
|*オートメーションプロジェクトイベント*|REG_SZ|イベント オブジェクトの名前。|キー名のみが関連します。 データ フィールドを使用してドキュメントを作成できます。<br /><br /> この例は、基本プロジェクトサンプルから取得されます。|
|*イベント*|REG_SZ|イベントオブジェクトの名前|キー名のみが関連します。 データ フィールドを使用してドキュメントを作成できます。<br /><br /> この例は、基本プロジェクトサンプルから取得されます。|

 オートメーション コンシューマーによってイベント オブジェクトが要求された場合は、VSPackage がサポートするイベントのメソッドを持つルート オブジェクトを作成します。 環境は、このオブジェクト`get_`に対して適切なメソッドを呼び出します。 たとえば、呼び`DTE.Events.AutomationProjectsEvents`出された場合、`get_AutomationProjectsEvents`ルート オブジェクトのメソッドが呼び出されます。

 ![プロジェクト イベント](../../extensibility/internals/media/projectevents.gif "ProjectEvents")イベントのオートメーションモデル

 クラス`CProjectEventsContainer`は *、Bsc プロジェクトイベント*のソース オブジェクトを`CProjectItemsEventsContainer`表し *、Bsc プロジェクトイベント イベント*のソース オブジェクトを表します。

 ほとんどのイベント オブジェクトはフィルタ オブジェクトを受け取るので、ほとんどの場合、イベントリクエストごとに新しいオブジェクトを返す必要があります。 イベントを発生させる場合は、このフィルターをチェックして、イベント ハンドラーが呼び出されていることを確認します。

 *次*の表に示すクラスの宣言と実装*が含まれています*。

|クラス|説明|
|-----------|-----------------|
|`CAutomationEvents`|オブジェクトから取得したイベント ルート オブジェクトを`DTE.Events`実装します。|
|`CProjectsEventsContainer` および `CProjectItemsEventsContainer`|対応するイベントを発生させるイベント ソース オブジェクトを実装します。|

 イベント オブジェクトの要求に応答する方法を次のコード例に示します。

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

 上記のコードでは、`g_wszAutomationProjects`プロジェクト コレクションの名前 (*FigProjects* `g_wszAutomationProjectsEvents` ) (*FigProjectsEvents*) および`g_wszAutomationProjectItemsEvents`(*FigProjectItemEvents*) は、VSPackage 実装からソースされるプロジェクト イベントとプロジェクト項目イベントの名前です。

 イベント オブジェクトは、同じ中央の場所であるオブジェクト`DTE.Events`から取得されます。 これにより、すべてのイベント オブジェクトがグループ化されるため、エンド ユーザーはオブジェクト モデル全体を参照して特定のイベントを検索する必要が生じないようにします。 また、システム全体のイベントに対して独自のコードを実装する代わりに、特定の VSPackage オブジェクトを提供することもできます。 ただし、`ProjectItem`インターフェイスのイベントを検索する必要があるエンド ユーザーの場合、そのイベント オブジェクトが取得される場所がすぐには明らかではありません。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
