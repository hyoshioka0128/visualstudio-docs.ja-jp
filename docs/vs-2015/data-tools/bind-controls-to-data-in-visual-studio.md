---
title: コントロールをデータにバインドする
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- displaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
caps.latest.revision: 42
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 31e2086126e9a17554c80b53858205e83fd504fd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673032"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>Visual Studio でのデータへのコントロールのバインド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データをコントロールにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインドコントロールを作成するには、[ **データソース** ] ウィンドウから Visual Studio のサーフェイス上のデザインサーフェイスまたはコントロールに項目をドラッグします。

 ここでは、データ バインディング コントロールを作成するために使用できるデータ ソースについて説明します。 また、データ バインディングに関連する一般的なタスクについても説明します。 データバインドコントロールの作成方法の詳細については、「 [Visual studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) 」と「 [visual studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

## <a name="data-sources"></a>データ ソース
 データバインディングのコンテキストでは、データソースは、ユーザーインターフェイスにバインドできるメモリ内のデータを表します。 実際には、データソースは、Entity Framework クラス、データセット、.NET プロキシオブジェクト、LINQ to SQL クラス、または任意の .NET オブジェクトまたはコレクションにカプセル化されたサービスエンドポイントにすることができます。 一部のデータ ソースでは、**[データ ソース]** ウィンドウから項目をドラッグすることによりデータ バインディング コントロールを作成できますが、その他のデータ ソースではできません。 サポートされるデータ ソースを次の表に示します。

|データ ソース|**Windows フォーム デザイナー**でのドラッグ アンド ドロップのサポート|**WPF デザイナー**でのドラッグ アンド ドロップのサポート|**Silverlight デザイナー**でのドラッグ アンド ドロップのサポート|
|-----------------|---------------------------------------------------------------|-----------------------------------------------------|-------------------------------------------------------------|
|データセット|はい|はい|いいえ|
|エンティティ データ モデル|可<sup>1</sup>|はい|はい|
|LINQ to SQL クラス|いいえ<sup>2</sup>|いいえ<sup>2</sup>|いいえ<sup>2</sup>|
|サービス ([!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]、WCF サービス、および Web サービスを含む)|はい|はい|はい|
|Object|はい|はい|はい|
|SharePoint|はい|はい|はい|

 1. **Entity Data Model**ウィザードを使用してモデルを生成し、それらのオブジェクトをデザイナーにドラッグします。

 2. LINQ to SQL クラスは、**[データ ソース]** ウィンドウに表示されません。 ただし、LINQ to SQL クラスに基づく新しいオブジェクト データ ソースを追加し、それらのオブジェクトをデザイナーにドラッグして、データ バインディング コントロールを作成できます。 詳細については、「 [チュートリアル: LINQ to SQL クラスの作成 (O/R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)」を参照してください。

## <a name="data-sources-window"></a>[データ ソース] ウィンドウ
 データ ソースは、**[データ ソース]** ウィンドウ内の項目としてプロジェクトで利用できます。 このウィンドウは、フォームデザインサーフェイスがプロジェクトのアクティブウィンドウである場合に表示されるか、[ **表示** ] メニューからアクセスできます。 このウィンドウから項目をドラッグして、基になるデータにバインドされたコントロールを作成することができます。また、データソースを構成するには、右クリックします。

 ![データソースウィンドウ](../data-tools/media/raddata-data-sources-window.png ""レーダーデータデータソース" ウィンドウ")

 **[データ ソース]** ウィンドウに表示されるデータ型ごとに、項目をデザイナーにドラッグしたときに既定のコントロールが作成されます。 [ **データソース** ] ウィンドウから項目をドラッグする前に、作成されるコントロールを変更できます。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

## <a name="tasks-involved-in-binding-controls-to-data"></a>データへのコントロールのバインドに関連するタスク
 次の表に、コントロールをデータにバインドするために実行する最も一般的なタスクの一部を示します。

|タスク|説明|
|----------|----------------------|
|**[データ ソース]** ウィンドウを開く。|エディターでデザインサーフェイスを開き、[ **View**  >  **データソース**の表示] を選択します。|
|プロジェクトにデータ ソースを追加する。|[新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)|
|**[データ ソース]** ウィンドウからデザイナーに項目をドラッグしたときに作成されるコントロールを設定する。|[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|**[データ ソース]** ウィンドウの項目に関連付けられるコントロールのリストを変更する。|[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|データ バインド コントロールを作成する。|[Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)|
|オブジェクトまたはコレクションにバインドします。|[Visual Studio でのオブジェクトのバインド](../data-tools/bind-objects-in-visual-studio.md)|
|UI に表示されるデータをフィルター処理します。|[Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|コントロールのキャプションをカスタマイズします。|[Visual Studio がデータ バインド コントロールのキャプションを作成する方法をカスタマイズする](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>参照
 [Visual Studio data tools for .net](../data-tools/visual-studio-data-tools-for-dotnet.md) [Windows フォームデータバインディング](https://msdn.microsoft.com/library/c3826d8e-ea25-4ad4-a669-45bfb19192aa)
