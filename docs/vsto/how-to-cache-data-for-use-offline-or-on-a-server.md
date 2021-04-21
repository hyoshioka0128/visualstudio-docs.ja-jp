---
title: '方法: オフラインまたはサーバーで使用するデータをキャッシュする'
description: データ項目がドキュメントにキャッシュされるようにマークして、オフラインで使用できるようにします。 これにより、ドキュメント内のデータを他のコードによって操作できるようになります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], server use
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- offline data [Office development in Visual Studio]
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio], offline use
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 07d7a33d90fd9d05c041ddc27f92a5b6a59bb75e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825993"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>方法: オフラインまたはサーバーで使用するデータをキャッシュする
  データ項目がドキュメントにキャッシュされるようにマークして、オフラインで使用できるようにすることができます。 これにより、ドキュメントがサーバーに格納されている場合に、ドキュメント内のデータを他のコードで操作することも可能になります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 データ項目がコード内で宣言されている場合、またはを使用している場合は、[ <xref:System.Data.DataSet> **プロパティ** ] ウィンドウでプロパティを設定することにより、データ項目がキャッシュされるようにマークすることができます。 またはではないデータ項目をキャッシュする場合 <xref:System.Data.DataSet> は <xref:System.Data.DataTable> 、ドキュメントにキャッシュされている条件を満たしていることを確認します。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

> [!NOTE]
> Cache および **WithEvents** とマークされている Visual Basic を使用 **して作成** されたデータセット ([**データソース**] ウィンドウまたは **CacheInDocument** プロパティが **True** に設定されている **ツールボックス** からドラッグしたデータセットを含む) には、キャッシュ内の名前の先頭にアンダースコアが付きます。 たとえば、データセットを作成して **Customers** という名前を指定した場合、その <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> 名前はキャッシュに **_Customers** されます。 を使用してこのキャッシュされた項目にアクセスする場合は <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 、**顧客** の代わりに **_Customers** を指定する必要があります。

### <a name="to-cache-data-in-the-document-using-code"></a>コードを使用してドキュメントのデータをキャッシュするには

1. データ項目のパブリックフィールドまたはプロパティをプロジェクト内のホスト項目クラスのメンバーとして宣言し `ThisDocumen` ます。たとえば、Word プロジェクトの t クラスや `ThisWorkbook` Excel プロジェクトのクラスなどです。

2. メンバーに属性を適用して、 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> ドキュメントのデータキャッシュに格納されるデータ項目をマークします。 次の例では、のフィールド宣言にこの属性を適用し <xref:System.Data.DataSet> ます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet11":::

3. データ項目のインスタンスを作成し、必要に応じてデータベースから読み込むコードを追加します。

     データ項目は、最初に作成されたときにのみ読み込まれます。その後、キャッシュはドキュメントと共に保持されます。更新するには、他のコードを記述する必要があります。

### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>プロパティウィンドウを使用してドキュメント内のデータセットをキャッシュするには

1. Visual Studio デザイナーのツールを使用して、データセットをプロジェクトに追加します。たとえば、[ **データソース** ] ウィンドウを使用してプロジェクトにデータソースを追加します。

2. データセットのインスタンスをまだ作成していない場合は作成し、デザイナーでインスタンスを選択します。

3. [ **プロパティ** ] ウィンドウで、 **CacheInDocument** プロパティを **True** に設定します。

     詳細については、「 [Office プロジェクトのプロパティ](../vsto/properties-in-office-projects.md)」を参照してください。

4. [ **プロパティ** ] ウィンドウで、[ **修飾子** ] プロパティを **Public** (既定では **Internal**) に設定します。

## <a name="see-also"></a>関連項目
- [キャッシュ データ](../vsto/caching-data.md)
- [方法: Office ドキュメント内のデータソースをプログラムによってキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [方法: パスワードで保護されたドキュメントでデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)
- [データを保存する](../data-tools/save-data-back-to-the-database.md)
