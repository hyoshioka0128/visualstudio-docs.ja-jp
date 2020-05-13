---
title: Web サービス テストを作成する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, creating Web service tests
- Web services [Visual Studio ALM], creating
- service tests, Web
ms.assetid: fbcd57ee-06ad-4260-8694-09f8e0f93e39
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7a6e42d6d92a74a0fc8be96c966b9146b7888b9e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589098"
---
# <a name="how-to-create-a-web-service-test"></a>方法: Web サービス テストを作成する

Web パフォーマンス テストを使用して、Web サービスをテストできます。 **[要求の挿入]** オプションおよび **[Web サービス要求の挿入]** オプションを使用すると、**Web パフォーマンス テスト エディター**にある個々の要求を Web サービス ページに移動するようにカスタマイズできます。 通常、Web アプリケーションでは、これらのページは表示されません。 そのため、これらのページへアクセスできるように要求をカスタマイズする必要があります。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

次の手順では、コマース スタート キットに含まれる Web サービスを使用します。 これは [ASP.NET コマース スタート キット](https://sourceforge.net/projects/ppcsk/)からダウンロードできます。

**必要条件**

Visual Studio Enterprise

## <a name="to-test-a-web-service"></a>Web サービスをテストするには

1. 新しい Web パフォーマンス テストを作成します。 ブラウザーが開いたら、すぐに **[停止]** を選択します。

2. **Web パフォーマンス テスト エディター**で、Web パフォーマンス テストを右クリックし、 **[Web サービス要求の追加]** を選択します。

3. 新しい要求の **[URL]** のプロパティで、 **http://localhost/storecsvs/InstantOrder.asmx** などの Web サービスの名前を入力します。

4. 別のセッションのブラウザーを開き、 **[アドレス]** ツール バーに *.asmx* ページの URL を入力します。 テストするメソッドを選択して、SOAP メッセージを調べます。 これには、`SOAPAction` が含まれます。

5. **Web パフォーマンス テスト エディター**で、要求を右クリックし、 **[ヘッダーの追加]** を選択して新しいヘッダーを追加します。 **[名前]** プロパティに「`SOAPAction`」と入力します。 **[値]** プロパティで、`SOAPAction` の値 (`"http://tempuri.org/CheckStatus"` など) を入力します。

6. エディタの URL ノードを展開し、 **[文字列ボディ]** ノードを選択して **[コンテンツの種類]** プロパティの値として「`text/xml`」と入力します。

7. 手順 4 のブラウザーに戻り、[Web サービスの説明] ページから SOAP 要求の XML 部分を選択し、クリップボードにコピーします。

8. 次に示すのは、XML の内容の一例です。

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
     <soap:Body>
       <CheckStatus xmlns="http://tempuri.org/">
         <userName>string</userName>
         <password>string</password>
         <orderID>int</orderID>
       </CheckStatus>
     </soap:Body>
     </soap:Envelope>
     ```

9. **Web パフォーマンス テスト エディター**に戻り、 **[文字列ボディ]** プロパティで省略記号 **(...)** を選択します。 クリップボードの内容をプロパティに貼り付けます。

10. テストを成功させるためには、XML に含まれているプレースホルダー値を有効な値に置き換える必要があります。 前のサンプルでは、2 つの `string` と 1 つの `int` を置換することになります。 この Web サービスの操作は、注文をした登録ユーザーが存在する場合にのみ完了します。

11. Web サービス要求を右クリックし、 **[URL QueryString パラメーターの追加]** を選択します。

12. クエリ文字列パラメーターに名前と値を代入します。 前の例では、名前は `op` となり、値は `CheckStatus` となります。 これは、実行される Web サービスの操作を識別します。

    > [!NOTE]
    > SOAP 本体のデータ バインディングを使用すると、`{{DataSourceName.TableName.ColumnName}}` 構文を使用して、プレースホルダー値をデータ バインディングされた値に置換できます。

13. テストを実行します。 **Web パフォーマンス テスト結果ビューアー**の上部ペインで、Web サービス要求を選択します。 下部ペインで、[Web ブラウザー] タブを選択します。Web サービスによって返された XML とあらゆる操作の結果とが表示されます。

## <a name="see-also"></a>関連項目

- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
