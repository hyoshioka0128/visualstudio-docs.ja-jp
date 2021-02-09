---
title: データセットデザイナーに DataTable を作成する
description: このチュートリアルでは、データセットデザイナーを使用して、(TableAdapter のない) DataTable を作成します。 新しい Windows フォームアプリケーションを作成し、新しいデータセットを追加します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: feec31fa0a9e34ad63e0b849d09084081e5710e5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858177"
---
# <a name="walkthrough-create-a-datatable-in-the-dataset-designer"></a>チュートリアル: データセットデザイナーでの DataTable の作成

このチュートリアルでは、 <xref:System.Data.DataTable> **データセットデザイナー** を使用して (TableAdapter を使用せずに) を作成する方法について説明します。 Tableadapter を含むデータテーブルの作成の詳細については、「 [tableadapter の作成と構成](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

## <a name="create-a-new-windows-forms-application"></a>新しい Windows フォーム アプリケーションを作成する

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ**] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに「 **Datatablewalkthrough**」という名前を入力し、[ **OK]** をクリックします。

     **Datatablewalkthrough** プロジェクトが作成され、**ソリューションエクスプローラー** に追加されます。

## <a name="add-a-new-dataset-to-the-application"></a>アプリケーションに新しいデータセットを追加する

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. 左側のウィンドウで、[ **データ**] を選択し、中央のペインで [データ **セット** ] を選択します。

3. **[追加]** をクリックします。

     Visual Studio によって、 **DataSet1** という名前のファイルがプロジェクトに追加され、 **データセットデザイナー** で開かれます。

## <a name="add-a-new-datatable-to-the-dataset"></a>新しい DataTable をデータセットに追加します。

1. **ツールボックス** の [**データセット**] タブから **DataTable** を **データセットデザイナー** にドラッグします。

     **DataTable1** という名前のテーブルがデータセットに追加されます。

2. **DataTable1** のタイトルバーをクリックし、名前を変更 `Music` します。

## <a name="add-columns-to-the-datatable"></a>DataTable への列の追加

1. [ **Music** ] テーブルを右クリックします。 **[追加]** をポイントして、**[列]** をクリックします。

2. 列にという名前を指定 `SongID` します。

3. **[プロパティ]** ウィンドウで、 <xref:System.Data.DataColumn.DataType%2A> プロパティを <xref:System.Int16?displayProperty=fullName>に設定します。

4. このプロセスを繰り返し、次の列を追加します。

     `SongTitle`: <xref:System.String?displayProperty=fullName>

     `Artist`: <xref:System.String?displayProperty=fullName>

     `Genre`: <xref:System.String?displayProperty=fullName>

## <a name="set-the-primary-key-for-the-table"></a>テーブルの主キーの設定

すべてのデータテーブルには主キーが必要です。 主キーは、データテーブル内の特定のレコードを一意に識別します。

主キーを設定するには、[ **SongID** ] 列を右クリックし、[ **主キーの設定**] をクリックします。 **SongID** 列の横にキーアイコンが表示されます。

## <a name="save-your-project"></a>プロジェクトを保存する

**Datatablewalkthrough** プロジェクトを保存するには、[**ファイル**] メニューの [**すべてを保存**] をクリックします。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータセットを作成および構成する](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [検証 (データを)](../data-tools/validate-data-in-datasets.md)
