---
title: プログラムによる Office ドキュメント内のデータソースのキャッシュ
description: ホスト項目の StartCaching メソッドを呼び出すことによって、プログラムを使用してデータオブジェクトをドキュメント内のデータキャッシュに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- StartCaching method
- data caching [Office development in Visual Studio], programmatically
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c0b739a7671f19b126b0566dfc8f4775a2c91063
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845013"
---
# <a name="how-to-programmatically-cache-a-data-source-in-an-office-document"></a>方法: Office ドキュメント内のデータソースをプログラムによってキャッシュする
  、、など `StartCaching` のホスト項目のメソッドを呼び出すことによって、プログラムを使用してデータオブジェクトをドキュメント内のデータキャッシュに追加でき <xref:Microsoft.Office.Tools.Word.Document> <xref:Microsoft.Office.Tools.Excel.Workbook> <xref:Microsoft.Office.Tools.Excel.Worksheet> ます。 ホスト項目のメソッドを呼び出すことによって、データキャッシュからデータオブジェクトを削除 `StopCaching` します。

 `StartCaching`メソッドとメソッドは `StopCaching` どちらもプライベートですが、IntelliSense に表示されます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 メソッドを使用してデータ `StartCaching` オブジェクトをデータキャッシュに追加する場合、データオブジェクトを属性で宣言する必要はありません <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 。 ただし、データオブジェクトは、データキャッシュに追加する特定の要件を満たしている必要があります。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

## <a name="to-programmatically-cache-a-data-object"></a>データオブジェクトをプログラムでキャッシュするには

1. データオブジェクトは、メソッドの内部ではなく、クラスレベルで宣言します。 この例では、 <xref:System.Data.DataSet> プログラムによってキャッシュするという名前のを宣言していることを前提としてい `dataSet1` ます。

     [!code-csharp[Trin_VstcoreDataExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#12)]
     [!code-vb[Trin_VstcoreDataExcel#12](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#12)]

2. データオブジェクトをインスタンス化し、 `StartCaching` ドキュメントまたはワークシートインスタンスのメソッドを呼び出して、データオブジェクトの名前を渡します。

     [!code-csharp[Trin_VstcoreDataExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#13)]
     [!code-vb[Trin_VstcoreDataExcel#13](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#13)]

## <a name="to-stop-caching-a-data-object"></a>データオブジェクトのキャッシュを停止するには

1. `StopCaching`ドキュメントまたはワークシートインスタンスのメソッドを呼び出し、データオブジェクトの名前を渡します。 この例では、 <xref:System.Data.DataSet> キャッシュを停止するという名前のがあることを前提としてい `dataSet1` ます。

     [!code-csharp[Trin_VstcoreDataExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#14)]
     [!code-vb[Trin_VstcoreDataExcel#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#14)]

    > [!NOTE]
    > `StopCaching` `Shutdown` ドキュメントまたはワークシートのイベントのイベントハンドラーからを呼び出さないでください。 イベントが発生した時点までに `Shutdown` 、データキャッシュを変更するには遅すぎます。 イベントの詳細については `Shutdown` 、「 [Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [キャッシュ データ](../vsto/caching-data.md)
- [方法: オフラインまたはサーバーで使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [方法: パスワードで保護されたドキュメントでデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)
- [データを保存する](../data-tools/save-data-back-to-the-database.md)
