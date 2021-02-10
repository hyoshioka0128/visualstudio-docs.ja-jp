---
title: データの視覚化と表示 |Microsoft Docs
description: 型ビジュアライザーとカスタムビューアーが開発者にデータを表示する方法について説明します。 式エバリュエーターでは、サードパーティの型ビジュアライザーがサポートされています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 61c2094564ea20c1073a198c3da162862c543e65
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965357"
---
# <a name="visualizing-and-viewing-data"></a>データの視覚化と表示
型ビジュアライザーおよびカスタムビューアーは、開発者にとってすぐに意味のある方法でデータを表示します。 式エバリュエーター (EE) では、サードパーティの型ビジュアライザーをサポートするだけでなく、独自のカスタムビューアーを指定することもできます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)][GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)メソッドを呼び出すことによって、オブジェクトの型に関連付けられている型ビジュアライザーおよびカスタムビューアーの数を決定します。 少なくとも1つの型ビジュアライザーまたはカスタムビューアーが使用可能な場合、Visual Studio は [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) メソッドを呼び出して、ビジュアライザーとビューアー (実際にはビジュアライザーとビューアーを実装するのリスト) のリストを取得し、ユーザーに提示します。

## <a name="supporting-type-visualizers"></a>型ビジュアライザーのサポート
 型ビジュアライザーをサポートするために EE が実装する必要があるインターフェイスがいくつかあります。 これらのインターフェイスは、型ビジュアライザーとプロパティデータにアクセスするインターフェイスを一覧表示するインターフェイスの2つの広範なカテゴリに分類できます。

### <a name="listing-type-visualizers"></a>リスト型ビジュアライザー
 EE は、およびの実装における型ビジュアライザーの一覧表示をサポートしてい `IDebugProperty3::GetCustomViewerCount` `IDebugProperty3::GetCustomViewerList` ます。 これらのメソッドは、対応するメソッド [GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) と [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)に呼び出しを渡します。

 [Ieevisualizerservice](../../extensibility/debugger/reference/ieevisualizerservice.md)は、 [createvisualizerservice](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)を呼び出すことによって取得されます。 このメソッドには、 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に渡される[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)インターフェイスから取得される[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)インターフェイスが必要です。 `IEEVisualizerServiceProvider::CreateVisualizerService` には、に渡された [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイスと [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) インターフェイスも必要です `IDebugParsedExpression::EvaluateSync` 。 インターフェイスを作成するために必要な最後のインターフェイス `IEEVisualizerService` は、EE が実装する [Ieevisualizerdataprovider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイスです。 このインターフェイスを使用すると、視覚化されるプロパティに変更を加えることができます。 すべてのプロパティデータは [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) インターフェイスにカプセル化されます。これは、EE によっても実装されます。

### <a name="accessing-property-data"></a>プロパティデータへのアクセス
 プロパティデータへのアクセスは、 [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスを介して行われます。 このインターフェイスを取得するために、Visual Studio はプロパティオブジェクトに対して[QueryInterface](/cpp/atl/queryinterface)を呼び出し、( [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを実装する同じオブジェクトに実装されている) [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)インターフェイスを取得してから、 [getpropertyproxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)メソッドを呼び出してインターフェイスを取得し `IPropertyProxyEESide` ます。

 インターフェイスに渡されるすべてのデータ `IPropertyProxyEESide` は、 [Ieedatastorage](../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスにカプセル化されます。 このインターフェイスはバイトの配列を表し、Visual Studio と EE の両方によって実装されます。 プロパティのデータを変更すると、Visual Studio は `IEEDataStorage` 新しいデータを保持するオブジェクトを作成し、そのデータオブジェクトを使用して[CreateReplacementObject](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)を呼び出します。新しいオブジェクトを取得して、 `IEEDataStorage` プロパティ[](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)のデータを更新します。 `IPropertyProxyEESide::CreateReplacementObject` インターフェイスを実装する独自のクラスを EE がインスタンス化できるようにし `IEEDataStorage` ます。

## <a name="supporting-custom-viewers"></a>カスタムビューアーのサポート
 フラグ `DBG_ATTRIB_VALUE_CUSTOM_VIEWER` は、 `dwAttrib` オブジェクトにカスタムビューアーが関連付けられていることを示す [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 構造体 ( [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)の呼び出しによって返される) のフィールドに設定されます。 このフラグが設定されている場合、Visual Studio は[QueryInterface](/cpp/atl/queryinterface)を使用して[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスから[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを取得します。

 ユーザーがカスタムビューアーを選択すると、Visual Studio は、 `CLSID` メソッドによって提供されるビューアーを使用して、カスタムビューアーをインスタンス化し `IDebugProperty3::GetCustomViewerList` ます。 次に、Visual Studio は [Displayvalue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) を呼び出して、ユーザーに値を表示します。

 通常、では、 `IDebugCustomViewer::DisplayValue` データの読み取り専用ビューが表示されます。 データの変更を許可するには、EE はプロパティオブジェクトのデータ変更をサポートするカスタムインターフェイスを実装する必要があります。 メソッドは、 `IDebugCustomViewer::DisplayValue` このカスタムインターフェイスを使用して、データの変更をサポートします。 メソッドは、 `IDebugProperty2` 引数として渡されたインターフェイスでカスタムインターフェイスを検索し `pDebugProperty` ます。

## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>型ビジュアライザーとカスタムビューアーの両方のサポート
 EE は、 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) メソッドと [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) メソッドで、型ビジュアライザーとカスタムビューアーの両方をサポートできます。 まず、EE は、提供しているカスタムビューアーの数を、 [GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) メソッドによって返される値に追加します。 次に、EE は、 `CLSID` [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) メソッドによって返されるリストに、独自のカスタムビューアーのを追加します。

## <a name="see-also"></a>関連項目
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
- [型ビジュアライザーとカスタムビューアー](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
