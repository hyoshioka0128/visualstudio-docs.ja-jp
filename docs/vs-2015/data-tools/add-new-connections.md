---
title: 新しい接続の追加 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 8a93c287-2834-4a83-a590-bdc3fe8d293f
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 44146613fb43b6fc4269741ba09b94629f888d5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673074"
---
# <a name="add-new-connections"></a>新しい接続を追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データベースまたはサービスへの接続をテストし、 **サーバーエクスプローラー**、 **Cloud Explorer**、または **SQL Server オブジェクトエクスプローラー**を使用して、データベースの内容とスキーマを調べることができます。 これらのウィンドウの機能は、いくつかの範囲に重なっています。 基本的な違いは次のとおりです。

 サーバーエクスプローラー、Visual Studio に既定でインストールされます。 を使用すると、接続をテストし、SQL Server データベース、ADO.NET プロバイダーがインストールされている他のデータベース、および一部の Azure サービスを表示できます。 また、システムパフォーマンスカウンター、イベントログ、メッセージキューなどの下位レベルのオブジェクトも表示されます。 データソースに ADO.NET プロバイダーがない場合は、ここに表示されませんが、プログラムによって接続することで、Visual Studio から使用することができます。

 [**ツール**] [  >  **拡張機能と更新プログラム**] [オンライン] [  >  **Online**  >  **visual studio ギャラリー**] の順に選択して、visual studio 拡張機能としてこのウィンドウを手動でインストール Cloud Explorer ます。 Azure サービスを探索して接続するための特別な機能を提供します。

 SQL Server オブジェクトエクスプローラー SQL Server Data Tools と共にインストールされ、[ **表示** ] メニューに表示されます。 表示されない場合は、コントロールパネルの [ **プログラムと機能** ] に移動し、[Visual Studio] を見つけて、[ **変更** ] を選択して、[SQL Server Data Tools] のチェックボックスをオンにしてインストーラーを再実行します。 **SQL Server オブジェクトエクスプローラー**を使用すると、SQL データベース (ADO.NET プロバイダーがある場合) を表示したり、新しいデータベースを作成したり、スキーマを変更したり、ストアドプロシージャを作成したり、接続文字列を取得したり、データを表示したりすることができます。 ADO.NET プロバイダーがインストールされていない SQL データベースはここに表示されませんが、プログラムによってそれらに接続することはできます。

## <a name="add-a-connection-in-server-explorer"></a>サーバーエクスプローラーに接続を追加する
 データベースへの接続を作成するには、**サーバーエクスプローラー**の [**接続の追加**] アイコンをクリックするか、[**データ接続**] ノードで**サーバーエクスプローラー**を右クリックして [**接続の追加**] を選択します。 ここでは、別のサーバー、SharePoint サービス、または Azure サービスのデータベースに接続することもできます。

 ![サーバーエクスプローラー新しい接続] アイコン](../data-tools/media/raddata-server-explorer-new-connection-icon.png "新しい接続アイコンサーバーエクスプローラーの [レーダーデータ]")

 [ **接続の追加** ] ダイアログボックスが表示されます。 ここでは、SQL Server LocalDB インスタンスの名前を入力しました。

 ![新しい接続の追加](../data-tools/media/raddata-add-new-connection-dialog.png "[新しい接続の追加] ダイアログボックスの [レーダーデータ]")

## <a name="change-the-provider"></a>プロバイダーを変更する
 データソースが不要な場合は、[ **変更** ] ボタンをクリックして、新しいデータソースや新しい ADO.NET データプロバイダーを選択します。 新しいプロバイダーは、構成方法に応じて、資格情報を要求する場合があります。

 ![AD0.NET Data Provider の変更](../data-tools/media/raddata-change-ad0-net-data-provider.png "AD0.NET Data Change Data Provider")

## <a name="test-the-connection"></a>接続をテストする
 データソースを選択したら、[ **接続テスト**] をクリックします。 成功しない場合は、ベンダーのドキュメントに基づいてトラブルシューティングを行う必要があります。

 ![[接続テスト]](../data-tools/media/raddata-test-connection.png "レーダーデータテスト接続")

 テストが成功すると、 *データソース*を作成する準備が整います。これは、基になるデータベースまたはサービスに基づく *データモデル* を意味する Visual Studio の用語です。

## <a name="see-also"></a>参照
 [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
