---
title: 新しい接続を追加する
ms.date: 11/04/2016
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 65c4e28eb9dfa3e3677f70d0557bb53ad8f9c3b2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587070"
---
# <a name="add-new-connections"></a>新しい接続を追加する

データベースまたはサービスへの接続をテストし、**サーバーエクスプローラー**、 **Cloud Explorer**、または**SQL Server オブジェクトエクスプローラー**を使用して、データベースの内容とスキーマを調べることができます。 これらのウィンドウの機能は、いくつかの範囲に重なっています。 基本的な違いは次のとおりです。

- サーバー エクスプローラー

   Visual Studio に既定でインストールされます。 を使用すると、接続をテストし、SQL Server データベース、ADO.NET プロバイダーがインストールされている他のデータベース、および一部の Azure サービスを表示できます。 また、システムパフォーマンスカウンター、イベントログ、メッセージキューなどの下位レベルのオブジェクトも表示されます。 データソースに ADO.NET プロバイダーがない場合は、ここに表示されませんが、プログラムによって接続することで、Visual Studio から使用することができます。

- Cloud Explorer

   このウィンドウは、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS)から Visual Studio 拡張機能として手動でインストールします。 Azure サービスを探索して接続するための特別な機能を提供します。

- SQL Server オブジェクト エクスプローラー

   SQL Server Data Tools と共にインストールされ、 **[表示]** メニューに表示されます。 表示されない場合は、コントロールパネルの **プログラムと機能** に移動し、Visual Studio を見つけて、**変更** を選択して、SQL Server Data Tools のチェックボックスをオンにしてインストーラーを再実行します。 **SQL Server オブジェクトエクスプローラー**を使用すると、SQL データベース (ADO.NET プロバイダーがある場合) を表示したり、新しいデータベースを作成したり、スキーマを変更したり、ストアドプロシージャを作成したり、接続文字列を取得したり、データを表示したりすることができます。 ADO.NET プロバイダーがインストールされていない SQL データベースはここに表示されませんが、プログラムによってそれらに接続することはできます。

## <a name="add-a-connection-in-server-explorer"></a>サーバーエクスプローラーに接続を追加する

データベースへの接続を作成するには、**サーバーエクスプローラー**の **[接続の追加]** アイコンをクリックするか、 **[データ接続]** ノードで**サーバーエクスプローラー**を右クリックして **[接続の追加]** を選択します。 ここでは、別のサーバー、SharePoint サービス、または Azure サービスのデータベースに接続することもできます。

![サーバーエクスプローラー新しい接続 アイコン](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

**[接続の追加]** ダイアログボックスが表示されます。 ここでは、SQL Server LocalDB インスタンスの名前を入力しました。

![新しい接続を追加する](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>プロバイダーを変更する

データソースが不要な場合は、 **[変更]** ボタンをクリックして、新しいデータソースや新しい ADO.NET データプロバイダーを選択します。 新しいプロバイダーは、構成方法に応じて、資格情報を要求する場合があります。

![AD0.NET Data Provider の変更](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>接続をテストする

データソースを選択したら、 **[接続テスト]** をクリックします。 成功しない場合は、ベンダーのドキュメントに基づいてトラブルシューティングを行う必要があります。

![[接続のテスト]](../data-tools/media/raddata-test-connection.png)

テストが成功すると、*データソース*を作成する準備が整います。これは、基になるデータベースまたはサービスに基づく*データモデル*を意味する Visual Studio の用語です。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
