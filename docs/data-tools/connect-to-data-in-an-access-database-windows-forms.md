---
title: Access データベース内のデータに接続する
description: Visual Studio で Access データベース (.mdb ファイルまたは .accdb ファイル) のデータに接続する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 07/18/2019
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting
- connecting to data, Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 156acfd56789ec13201738e72c6df283e257e94f
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436863"
---
# <a name="connect-to-data-in-an-access-database"></a>Access データベース内のデータに接続する

Visual Studio を使用して、Access データベース ( *.mdb* ファイルまたは *.accdb* ファイル) に接続できます。 接続を定義すると、 **[データ ソース ウィンドウ]** にデータが表示されます。 そこから、テーブルまたはビューをデザイン画面にドラッグすることができます。

## <a name="prerequisites"></a>前提条件

これらの手順を使用するには、Windows フォームまたは WPF プロジェクト、Access データベース ( *.accdb* ファイル)、または access 2000-2003 データベース ( *.mdb* ファイル) のいずれかが必要です。 ファイルの種類に対応する手順に従ってください。

## <a name="create-a-dataset-for-an-accdb-file"></a>.Accdb ファイルのデータセットを作成する

次の手順に従って、Microsoft 365、access 2013、Access 2010、または Access 2007 で作成されたデータベースに接続します。

1. Visual Studio で Windows フォームまたは WPF アプリケーションプロジェクトを開きます。

2. [ **データソース** ] ウィンドウを開くには、[ **表示** ] メニューの [ **その他の Windows**  >  **データソース** ] をクリックします。

   ![[表示]、[その他のウィンドウ]、[データ ソース]](../data-tools/media/viewdatasources.png)

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

   **データソース構成ウィザード** が開きます。

4. [ **データソースの種類を選択** ] ページで [ **データベース** ] を選択し、[ **次へ** ] を選択します。

5. [ **データベースモデルの選択** ] ページで [ **データセット** ] を選択し、[ **次へ** ] を選択します。

6. **[データ接続の選択]** ページで、 **[新しい接続]** を選択して新しいデータ接続を構成します。

   **[接続の追加]** ダイアログ ボックスが表示されます。

7. [ **データソース** ] が [ **Microsoft access データベースファイル** ] に設定されていない場合は、[ **変更** ] をクリックします。

   [ **データソースの変更** ] ダイアログボックスが表示されます。 データソースの一覧で、[ **Microsoft Access データベースファイル** ] を選択します。 [ **データプロバイダー** ] ドロップダウンで、[ **OLE DB の .NET Framework Data Provider** を選択し、[ **OK]** を選択します。

8. [ **データベースファイル名** ] の横にある [ **参照** ] をクリックし、 *.accdb* ファイルに移動して、[ **開く** ] を選択します。

9. 必要に応じて、ユーザー名とパスワードを入力し、[ **OK]** をクリックします。

10. [ **データ接続の選択** ] ページで [ **次へ** ] を選択します。

    データファイルが現在のプロジェクトに含まれていないことを示すダイアログボックスが表示される場合があります。 [ **はい]** または [ **いいえ** ] を選択します。

11. [ **アプリケーション構成ファイルに接続文字列を保存** ] ページで [ **次へ** ] を選択します。

12. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

13. データセットに含めるテーブルまたはビューを選択し、[ **完了** ] を選択します。

    プロジェクトにデータセットが追加され、テーブルとビューが **[データ ソース]** ウィンドウに表示されます。

## <a name="create-a-dataset-for-an-mdb-file"></a>.Mdb ファイルのデータセットを作成する

次の手順に従って、Access 2000-2003 で作成したデータベースに接続します。

1. Visual Studio で Windows フォームまたは WPF アプリケーションプロジェクトを開きます。

2. [ **表示** ] メニューの [ **その他の Windows**  >  **データソース** ] をクリックします。

   ![[表示]、[その他のウィンドウ]、[データ ソース]](../data-tools/media/viewdatasources.png)

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

    **データソース構成ウィザード** が開きます。

4. [ **データソースの種類を選択** ] ページで [ **データベース** ] を選択し、[ **次へ** ] を選択します。

5. [ **データベースモデルの選択** ] ページで [ **データセット** ] を選択し、[ **次へ** ] を選択します。

6. **[データ接続の選択]** ページで、 **[新しい接続]** を選択して新しいデータ接続を構成します。

7. データソースが **Microsoft Access データベースファイル (OLE DB)** でない場合は、[ **変更** ] を選択して [ **データソースの変更** ] ダイアログボックスを開き、[ **microsoft access データベースファイル** ] を選択し、[ **OK]** を選択します。

8. [ **データベースファイル名** ] に、接続先の *.mdb* ファイルのパスと名前を指定し、[ **OK]** を選択します。

   ![Access データベース ファイルへの接続を追加](../data-tools/media/add-connection-access-db.png)

9. [ **データ接続の選択** ] ページで [ **次へ** ] を選択します。

10. [ **アプリケーション構成ファイルに接続文字列を保存** ] ページで [ **次へ** ] を選択します。

11. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

12. データセット内の任意のテーブルまたはビューを選択し、[ **完了** ] を選択します。

    プロジェクトにデータセットが追加され、テーブルとビューが **[データ ソース]** ウィンドウに表示されます。

## <a name="next-steps"></a>次のステップ

先ほど作成したデータセットは、[ **データソース** ] ウィンドウで使用できます。 これで、以下のタスクをどれでも実行できます。

- [ **データソース** ] ウィンドウで項目を選択し、フォームまたはデザインサーフェイスにドラッグします (「 [Visual Studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) 」または「 [WPF データバインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)」を参照してください)。

- **データセット デザイナー** でデータ ソースを開き、データセットを構成しているオブジェクトを追加または編集します。

- データ <xref:System.Data.DataTable.ColumnChanging> セット内のデータテーブルのイベントまたはイベントに検証ロジックを追加し <xref:System.Data.DataTable.RowChanging> ます (「 [データセットのデータを検証](../data-tools/validate-data-in-datasets.md)する」を参照してください)。

## <a name="see-also"></a>関連項目

- [接続を追加する](../data-tools/add-new-connections.md)
- [WPF データバインディングの概要](/dotnet/framework/wpf/data/data-binding-overview)
- [データバインディングの Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)
