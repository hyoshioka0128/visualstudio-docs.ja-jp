---
title: Access データベースのデータに接続する (Windows フォーム) |Microsoft Docs
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
- databases, connecting to
- databases, Access
- data [Visual Studio], connecting
- connecting to data, from Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8426e9fcaa29bef36b6701c78d622f6f42fd1171
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651143"
---
# <a name="connect-to-data-in-an-access-database-windows-forms"></a>Access データベース内のデータへの接続 (Windows フォーム)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio を使用して、Access データベース (.mdf ファイルまたは .accdb ファイル) に接続できます。 接続を定義すると、**[データ ソース ウィンドウ]** にデータが表示されます。 ここから、テーブルまたはビューをフォームにドラッグできます。

## <a name="prerequisites"></a>前提条件
 これらの手順を使用するには、Windows フォームアプリケーションプロジェクト、Access データベース (.accdb ファイル)、または Access 2000-2003 データベース (.mdb ファイル) のいずれかが必要です。 ファイルの種類に対応する手順に従ってください。

## <a name="creating-the-dataset-for-an-accdb-file"></a>.accdb ファイルのデータセットの作成
 Access 2013、Office 365、Access 2010、または access 2007 を使用して作成されたデータベースに接続するには、次の手順を実行します。

#### <a name="to-create-the-dataset"></a>データセットを作成するには

1. データの接続先となる Windows フォーム アプリケーションを開きます。

2. [**表示**] メニューの [**その他の Windows**  >  **データソース**] をクリックします。

     ![[表示]、[その他のウィンドウ]、[データ ソース]](../data-tools/media/viewdatasources.png "ViewDataSources ソース")

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

     ![新しいデータソースの追加](../data-tools/media/dataaddnewdatasource.png "dataAddNewDataSource")

4. [**データソースの種類を選択**] ページで [**データベース**] を選択し、[**次へ**] を選択します。

5. [**データベースモデルの選択**] ページで [**データセット**] を選択し、[**次へ**] を選択します。

6. **[データ接続の選択]** ページで、**[新しい接続]** を選択して新しいデータ接続を構成します。

7. **データソース**を**OLE DB の .NET Framework Data Provider**に変更します。

     ![データ プロバイダーを OLE DB に変更](../data-tools/media/datachangedatasourceoledb.png "dataChangeDataSourceOLEDB")

    > [!IMPORTANT]
    > **Microsoft Access データベースファイル (OLE DB)** のデータソースは適切な選択のように思われるかもしれませんが、そのデータソースの種類は .mdb データベースファイルに対してのみ使用します。

8. **OLE DB プロバイダー**で、 **Microsoft Office 12.0 Access データベースエンジン OLE DB プロバイダー**] を選択します。

     ![OLE DB プロバイダーの Microsoft Office 12.0 Access](../data-tools/media/dataoledbprovideroffice12access.png "dataOLEDBProviderOffice12Access")

9. [ **サーバー名またはファイル名**] に、接続先の .accdb ファイルのパスと名前を指定し、[ **OK]** を選択します。

    > [!NOTE]
    > データベースファイルにユーザー名とパスワードが含まれている場合は、[ **OK]** を選択する前に指定します。

10. [**データ接続の選択**] ページで [**次へ**] を選択します。

11. [**アプリケーション構成ファイルに接続文字列を保存**] ページで [**次へ**] を選択します。

12. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

13. データセット内の任意のテーブルまたはビューを選択し、[ **完了**] を選択します。

     プロジェクトにデータセットが追加され、テーブルとビューが **[データ ソース]** ウィンドウに表示されます。

## <a name="creating-the-dataset-for-an-mdb-file"></a>.Mdb ファイルのデータセットの作成
 **データ ソース構成ウィザード**を実行して、データセットを作成します。

#### <a name="to-create-the-dataset"></a>データセットを作成するには

1. データの接続先となる Windows フォーム アプリケーションを開きます。

2. [**表示**] メニューの [**その他の Windows**  >  **データソース**] をクリックします。

     ![[表示]、[その他のウィンドウ]、[データ ソース]](../data-tools/media/viewdatasources.png "ViewDataSources ソース")

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

4. [**データソースの種類を選択**] ページで [**データベース**] を選択し、[**次へ**] を選択します。

5. [**データベースモデルの選択**] ページで [**データセット**] を選択し、[**次へ**] を選択します。

6. **[データ接続の選択]** ページで、**[新しい接続]** を選択して新しいデータ接続を構成します。

7. データソースが **Microsoft Access データベースファイル (OLE DB)** でない場合は、[ **変更** ] を選択して [ **データソースの変更** ] ダイアログボックスを開き、[ **microsoft access データベースファイル**] を選択し、[ **OK]** を選択します。

8. [ **データベースファイル名**] に、接続先の .mdb ファイルのパスと名前を指定し、[ **OK]** を選択します。

     ![Access データベース ファイルへの接続を追加](../data-tools/media/dataaddconnectionaccessmdb.png "dataAddConnectionAccessMDB")

9. [**データ接続の選択**] ページで [**次へ**] を選択します。

10. [**アプリケーション構成ファイルに接続文字列を保存**] ページで [**次へ**] を選択します。

11. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

12. データセット内の任意のテーブルまたはビューを選択し、[ **完了**] を選択します。

     プロジェクトにデータセットが追加され、テーブルとビューが **[データ ソース]** ウィンドウに表示されます。

## <a name="security"></a>セキュリティ
 機密情報 (パスワードなど) を格納すると、アプリケーションのセキュリティに影響を及ぼすことがあります。 データベースへのアクセスを制御する方法としては、Windows 認証 (統合セキュリティとも呼ばれます) を使用する方が安全です。 詳細については、「[接続情報の保護](https://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4)」を参照してください。

## <a name="next-steps"></a>次の手順
 先ほど作成したデータセットは、[ **データソース** ] ウィンドウで使用できるようになりました。 これで、以下のタスクをどれでも実行できます。

- [ **データソース** ] ウィンドウで項目を選択し、フォームにドラッグします (「 [Visual Studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」を参照してください)。

- データセット デザイナーでデータ ソースを開き、データセットを構成しているオブジェクトを追加または編集します。

- データ <xref:System.Data.DataTable.ColumnChanging> セット内のデータテーブルのイベントまたはイベントに検証ロジックを追加し <xref:System.Data.DataTable.RowChanging> ます (「 [データセットのデータを検証](../data-tools/validate-data-in-datasets.md)する」を参照してください)。

## <a name="see-also"></a>参照

 データを[受信するためのアプリケーションの準備](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad) [Visual Studio でのデータバインドコントロールデータデータの](../data-tools/bind-controls-to-data-in-visual-studio.md)[検証](https://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)の[チュートリアル](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)