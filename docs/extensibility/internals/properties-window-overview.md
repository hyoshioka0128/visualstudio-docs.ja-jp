---
title: プロパティウィンドウの概要 |Microsoft Docs
description: この概要では、Visual Studio IDE のプロパティウィンドウとの対話に使用するインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5f378200072df603817a445a9c3406cf62233c8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061005"
---
# <a name="properties-window-overview"></a>プロパティ ウィンドウの概要
[ **プロパティ** ] ウィンドウは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) で使用できる2つの主要な種類のウィンドウで選択されたオブジェクトのプロパティを表示するために使用されます。 この2種類のウィンドウは次のとおりです。

- ソリューションエクスプローラー、クラスビュー、オブジェクトブラウザーなどのツールウィンドウ

- フォームデザイナー、XML エディター、HTML エディターなどのエディターやデザイナーを含むドキュメントウィンドウ

## <a name="using-the-properties-window"></a>[プロパティ] ウィンドウの使用
 [ **プロパティ** ] ウィンドウには、1つまたは複数の選択した項目のプロパティが表示されます。 複数の項目が選択されている場合は、選択したすべてのオブジェクトのすべてのプロパティの共通部分が表示されます。

 [ **プロパティ** ] ウィンドウには、フォームデザインウィンドウまたは com + メタデータを使用した HTML エディターで、選択したオブジェクトに関連するイベントが表示されます。 たとえば、ボタンを選択して、関連付けられているイベント (イベントなど) を表示することができ `OnClick` ます。これは、そのボタンにリンクできます。

 [ **プロパティ** ] ウィンドウに表示されるイベントは、主にコードにバインドされているオブジェクトで使用されます。 コードで実行するものがないファイル形式を編集している場合、イベントは発生しません。 イベントは、実行中のコードと特定のオブジェクトに関連付けられている特定のイベントとの間にバインドがある場合にのみ、[ **プロパティ** ] ウィンドウに表示されます。 この例としては、選択したオブジェクトを、そのオブジェクトがアクティブになったときに実行するコードがあります。

 次の表に、[ **プロパティ** ] ウィンドウで使用される主なインターフェイスを示します。

|Interface Name|説明|
|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|[ **プロパティ** ] ウィンドウにカテゴリの一覧を表示し、各プロパティをカテゴリにマップします。|
|[IDispatch インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)|オブジェクトのメソッドとプロパティを、プログラミングツールや、オートメーションをサポートするその他のアプリケーションに公開します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|オブジェクト自体によって実装されたモーダルダイアログウィンドウを開く *ビルダー* と呼ばれる省略記号ボタン ([...]) を提供します。 ユーザーがテキストフィールドで値を簡単に入力できない場合に使用します。 たとえば、RGB 値を決定するカラーピッカーを開くために使用される場合があります。|
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|[ **プロパティ** ] ウィンドウに表示される情報を更新するために使用するオブジェクトへのアクセスを提供します。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、関連するプロパティを表示する選択可能なオブジェクトを含むウィンドウごとに Vspackage によって実装されます。|
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|インターフェイスのメソッドや構造体のフィールドなど、オブジェクトの型に関する情報を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|Vspackage が選択イベントの通知を受信し、現在のプロジェクト階層、項目、要素の値、およびコマンドの UI コンテキストに関する情報を取得できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|複数の選択にアクセスできる環境を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|[ **プロパティ** ] ウィンドウに表示されるいくつかのプロパティにローカライズされた名前を提供するために使用します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|現在の選択項目、要素の値、またはコマンドの UI コンテキストに対する変更について、登録されている Vspackage に通知します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|現在の選択範囲の変更を環境に通知し、新しい選択に関連する階層と項目情報へのアクセスを提供します。|

 の詳細については `IDispatch` 、MSDN ライブラリを参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
- [プロパティ ウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)
