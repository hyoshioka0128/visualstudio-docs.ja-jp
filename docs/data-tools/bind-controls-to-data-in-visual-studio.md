---
title: データ コントロールのバインド
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- displaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9e0746de34a16dc181baff3c8b843b123c2ae434
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587031"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>Visual Studio でのデータへのコントロールのバインド

データをコントロールにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインドコントロールを作成するには、 **[データソース]** ウィンドウから Visual Studio のサーフェイス上のデザインサーフェイスまたはコントロールに項目をドラッグします。

ここでは、データ バインディング コントロールを作成するために使用できるデータ ソースについて説明します。 また、データ バインディングに関連する一般的なタスクについても説明します。 データバインドコントロールの作成方法の詳細については、「 [Visual studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」と「 [visual studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

## <a name="data-sources"></a>データ ソース

データバインディングのコンテキストでは、データソースは、ユーザーインターフェイスにバインドできるメモリ内のデータを表します。 実際には、データソースは、Entity Framework クラス、データセット、.NET プロキシオブジェクト、LINQ to SQL クラス、または任意の .NET オブジェクトまたはコレクションにカプセル化されたサービスエンドポイントにすることができます。 一部のデータ ソースでは、 **[データ ソース]** ウィンドウから項目をドラッグすることによりデータ バインディング コントロールを作成できますが、その他のデータ ソースではできません。 サポートされるデータ ソースを次の表に示します。

| [データ ソース] | **Windows フォーム デザイナー**でのドラッグ アンド ドロップのサポート | **WPF デザイナー**でのドラッグ アンド ドロップのサポート | **Silverlight デザイナー**でのドラッグ アンド ドロップのサポート |
| - | - | - | - |
| データセット | ○ | ○ | いいえ |
| エンティティ データ モデル | ○<sup>1</sup> | ○ | ○ |
| LINQ to SQL クラス | ×<sup>2</sup> | ×<sup>2</sup> | ×<sup>2</sup> |
| サービス ([!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]、WCF サービス、および Web サービスを含む) | ○ | ○ | ○ |
| オブジェクト | ○ | ○ | ○ |
| SharePoint | ○ | ○ | ○ |

1. **Entity Data Model**ウィザードを使用してモデルを生成し、それらのオブジェクトをデザイナーにドラッグします。

2. LINQ to SQL クラスは、 **[データ ソース]** ウィンドウに表示されません。 ただし、LINQ to SQL クラスに基づく新しいオブジェクト データ ソースを追加し、それらのオブジェクトをデザイナーにドラッグして、データ バインディング コントロールを作成できます。 詳細については、「[チュートリアル: LINQ to SQL クラスの作成 (O/R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)」を参照してください。

## <a name="data-sources-window"></a>[データ ソース] ウィンドウ

データ ソースは、 **[データ ソース]** ウィンドウ内の項目としてプロジェクトで利用できます。 このウィンドウは、フォームデザインサーフェイスがプロジェクトのアクティブなウィンドウであるときに表示されます。または、[**他の Windows** > **データソース**を**表示** > ] を選択して開くことができます (プロジェクトが開いている場合)。 このウィンドウから項目をドラッグして、基になるデータにバインドされたコントロールを作成することができます。また、データソースを構成するには、右クリックします。

![[データ ソース] ウィンドウ](../data-tools/media/raddata-data-sources-window.png)

**[データ ソース]** ウィンドウに表示されるデータ型ごとに、項目をデザイナーにドラッグしたときに既定のコントロールが作成されます。 **[データソース]** ウィンドウから項目をドラッグする前に、作成されたコントロールを変更できます。 詳細については、「[[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

## <a name="tasks-involved-in-binding-controls-to-data"></a>データへのコントロールのバインドに関連するタスク

次の表に、コントロールをデータにバインドするために実行する最も一般的なタスクの一部を示します。

|タスク|説明|
|----------| - |
|**[データ ソース]** ウィンドウを開く。|エディターでデザインサーフェイスを開き、[ > **データソース**の**表示**] を選択します。|
|プロジェクトにデータ ソースを追加する。|[新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)|
|**[データ ソース]** ウィンドウからデザイナーに項目をドラッグしたときに作成されるコントロールを設定する。|[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|**[データ ソース]** ウィンドウの項目に関連付けられるコントロールのリストを変更する。|[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|データ バインド コントロールを作成する。|[Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)|
|オブジェクトまたはコレクションにバインドします。|[Visual Studio でのオブジェクトのバインド](../data-tools/bind-objects-in-visual-studio.md)|
|UI に表示されるデータをフィルター処理します。|[Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|コントロールのキャプションをカスタマイズします。|[Visual Studio がデータ バインド コントロールのキャプションを作成する方法をカスタマイズする](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Windows フォームでのデータ バインディング](/dotnet/framework/winforms/windows-forms-data-binding)
