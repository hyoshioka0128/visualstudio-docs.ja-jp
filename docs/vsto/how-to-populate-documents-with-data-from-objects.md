---
title: '方法: オブジェクトのデータをドキュメントに読み込む'
description: ソリューション内のオブジェクトのデータを使用する方法について説明します。また、Windows フォームコントロールを使用して、ドキュメント内のデータを表示することもできます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], populating with data
- data [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 73cc795b5476f312f5fc80ba76dc383175596b64
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96848054"
---
# <a name="how-to-populate-documents-with-data-from-objects"></a>方法: オブジェクトのデータをドキュメントに読み込む

Microsoft Office Word のドキュメント レベルのプロジェクトでは、Windows フォーム プロジェクトと同じ方法でデータ オブジェクトのデータにアクセスできます。 同じツールとコードを使用してオブジェクトからソリューションにデータを読み込むことができ、Windows フォーム コントロールを使用してデータを表示できます。 また、ホスト コントロールを使用してデータを表示することもできます。 ホスト コントロールは、イベントおよびデータ バインディングの機能が強化された Microsoft Office Word のネイティブ オブジェクトです。 詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

ドキュメントにオブジェクトのデータを読み込むには、次の 3 つの基本手順を実行する必要があります。

- データにバインドできるドキュメントにコントロールを追加する。

- データ オブジェクトをドキュメントに追加する。

- データ オブジェクトを BindingSource に接続する。

## <a name="to-add-a-data-object"></a>データ オブジェクトを追加するには

データオブジェクトを追加するには、[ **データソース** ] ウィンドウを開き、オブジェクトからデータソースを作成します。 詳細については、「[新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)」を参照してください。

## <a name="connect-the-data-object-to-the-bindingsource"></a>データオブジェクトを BindingSource に接続する

ドキュメント レベルのプロジェクトでは、デザイン時にコントロールを文書に追加し、そのコントロールをデータにバインドできます。

VSTO アドイン プロジェクトでは、コントロールを作成して、そのコントロールを実行時にバインドできます。

### <a name="document-level-projects"></a>ドキュメントレベルのプロジェクト

データオブジェクトを BindingSource に接続するには、次のようにします。

1. **[データ ソース]** ウィンドウから目的のデータ フィールドを文書にドラッグします これにより、コントロールが自動的に作成されます。

2. コードで、データ ソースとして選択したオブジェクトの種類のインスタンスを作成します。

3. このインスタンスを <xref:System.Windows.Forms.BindingSource.DataSource%2A> の <xref:System.Windows.Forms.BindingSource>プロパティに割り当てます。

### <a name="application-level-projects"></a>アプリケーションレベルのプロジェクト

データオブジェクトを BindingSource に接続するには、次のようにします。

1. コード中に、データ ソースに関連付けられているオブジェクトの種類のインスタンスを作成します。

2. <xref:System.Windows.Forms.BindingSource> のインスタンスを作成します。

3. データ ソースのインスタンスを <xref:System.Windows.Forms.BindingSource.DataSource%2A> の <xref:System.Windows.Forms.BindingSource>プロパティに割り当てます。

4. コントロールへのデータ バインディングとしてデータ ソースを追加します。

## <a name="see-also"></a>関連項目

- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: ホストコントロールのデータを使用してデータソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)