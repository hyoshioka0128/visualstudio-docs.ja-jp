---
title: データの視覚化と表示 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b5f984e6c6a3c1c8f3835dfa93a8679ae16680a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712371"
---
# <a name="visualizing-and-viewing-data"></a>データの視覚化と表示
型ビジュアライザーとカスタム ビューアーは、開発者にとってすぐに意味のある方法でデータを表示します。 式エバリュエーター (EE) は、サードパーティの種類のビジュアライザーをサポートするだけでなく、独自のカスタム ビューアーを提供できます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)][GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)メソッドを呼び出すことによって、オブジェクトの型に関連付けられている型ビジュアライザーとカスタム ビューアーの数を決定します。 少なくとも 1 つの型ビジュアライザーまたはカスタム ビューアーが使用可能な場合、Visual Studio は、それらのビジュアライザーとビューアー (実際には、ビジュアライザーとビューアーを実装するのリスト) のリストを取得するために[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)メソッドを呼び出し、ユーザーに提示します。

## <a name="supporting-type-visualizers"></a>サポート型ビジュアライザー
 型ビジュアライザーをサポートするために EE が実装する必要があるインターフェイスは多数あります。 これらのインターフェイスは、型ビジュアライザーをリストするインターフェイスとプロパティ データにアクセスするインターフェイスという 2 つの大きなカテゴリに分類できます。

### <a name="listing-type-visualizers"></a>リスト型ビジュアライザー
 EE は、 の実装で型ビジュア`IDebugProperty3::GetCustomViewerCount`ライザー`IDebugProperty3::GetCustomViewerList`の一覧表示をサポートしています。 これらのメソッドは、対応するメソッド[に](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)呼び出しを渡[します](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)。

 [IEE ビジュアライザー サービス](../../extensibility/debugger/reference/ieevisualizerservice.md)は、[ビジュアライザー サービス](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)を呼び出すことによって取得されます。 このメソッドには、[評価同期](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に渡される[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)インターフェイスから取得される[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)インターフェイスが必要です。 `IEEVisualizerServiceProvider::CreateVisualizerService`また、に渡された[インターフェイス](../../extensibility/debugger/reference/idebugsymbolprovider.md)と[IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)インターフェイスも必要です`IDebugParsedExpression::EvaluateSync`。 `IEEVisualizerService`インターフェイスを作成するために必要な最終的なインターフェイスは、EE が実装する[IEE ビジュアライザーデータ プロバイダー](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)インターフェイスです。 このインターフェイスを使用すると、視覚化されるプロパティに変更を加えます。 すべてのプロパティ データは、EE によって実装される[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)インターフェイスにカプセル化されます。

### <a name="accessing-property-data"></a>プロパティ データへのアクセス
 プロパティ データへのアクセスは、[インターフェイス](../../extensibility/debugger/reference/ipropertyproxyeeside.md)を介して行われます。 このインターフェイスを取得するには、プロパティ オブジェクトで[クエリ インターフェイス](/cpp/atl/queryinterface)を呼び出して[、IPropertyProxyProvider インターフェイス (IDebugProperty3](../../extensibility/debugger/reference/ipropertyproxyprovider.md)インターフェイス[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)を実装するオブジェクトに実装されている) を取得し[、GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) `IPropertyProxyEESide`メソッドを呼び出してインターフェイスを取得します。

 `IPropertyProxyEESide`インターフェイスに出入りするすべてのデータは[、IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)インターフェイスにカプセル化されます。 このインターフェイスはバイト配列を表し、Visual Studio と EE の両方によって実装されます。 プロパティのデータを変更する場合、Visual Studio は新しい`IEEDataStorage`データを保持するオブジェクトを作成し、そのデータ オブジェクトを使用して[CreateReplacementObject](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)を呼び出して、プロパティのデータを更新するために`IEEDataStorage`[InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)に渡される新しいオブジェクトを取得します。 `IPropertyProxyEESide::CreateReplacementObject`EE は、インターフェイスを実装する独自のクラスを`IEEDataStorage`インスタンス化できます。

## <a name="supporting-custom-viewers"></a>カスタム ビューアーのサポート
 このフラグ`DBG_ATTRIB_VALUE_CUSTOM_VIEWER`は、オブジェクトに`dwAttrib`カスタム ビューアーが関連付けられていることを示すために[、DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)構造体のフィールド[(GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)の呼び出しによって返される) に設定されます。 このフラグが設定されている場合、Visual Studio は[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用して[IDebugProperty2 インターフェイスから IDebugProperty3](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを取得します。 [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)

 ユーザーがカスタム ビューアーを選択すると、Visual Studio は、メソッドによって`CLSID`提供されるビューアーを使用してカスタム`IDebugProperty3::GetCustomViewerList`ビューアーをインスタンス化します。 次に、ユーザーに値を表示するために[DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)を呼び出します。

 通常は、`IDebugCustomViewer::DisplayValue`データの読み取り専用ビューを表示します。 データの変更を許可するには、EE はプロパティ オブジェクトのデータの変更をサポートするカスタム インターフェイスを実装する必要があります。 この`IDebugCustomViewer::DisplayValue`メソッドは、このカスタム インターフェイスを使用して、データの変更をサポートします。 メソッドは、引数として渡された`IDebugProperty2`インターフェイスのカスタム インターフェイスを検索`pDebugProperty`します。

## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>型ビジュアライザーとカスタム ビューアーの両方をサポート
 EE は、型ビジュアライザーとカスタム ビューアーの両方を[サポート](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)できます[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)。 最初に、EE は[、GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)メソッドによって返される値に、指定するカスタム ビューアーの数を追加します。 次に、EE は、`CLSID`独自のカスタム ビューアーの s を[GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)メソッドによって返されるリストに追加します。

## <a name="see-also"></a>関連項目
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
- [型ビジュアライザーとカスタム ビューアー](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
