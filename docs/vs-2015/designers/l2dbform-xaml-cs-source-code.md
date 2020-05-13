---
title: L2DBForm.xaml.cs ソース コード | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 5a40dad3-6763-4576-b3ad-874df3f2c8d9
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3f783161865092f714955b65e6f2fa4791741cbe
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664289"
---
# <a name="l2dbformxamlcs-source-code"></a>L2DBForm.xaml.cs Source Code
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、L2DBForm.xaml.cs ファイルの C# ソース コードの内容と説明を示します。 このファイルに含まれている L2XDBForm 部分クラスは、3 つの論理的な部分、つまりデータ メンバー、`OnRemove`、`OnAddBook` ボタン クリック イベント ハンドラーに分けることができます。

## <a name="data-members"></a>データ メンバー
 このクラスを L2DBForm.xaml で使用されているウィンドウ リソースに関連付けるために、2 つのプライベート データ メンバーが使用されています。

- 名前空間変数 `myBooks` は、`"http://www.mybooks.com"` に初期化されます。

- メンバー `bookList` は、コンストラクター内で次の行を使用して L2DBForm.xaml 内の CDATA 文字列に初期化されます。

    ```
    bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
    ```

## <a name="onaddbook-event-handler"></a>OnAddBook イベント ハンドラー
 このメソッドには次の 3 つのステートメントが含まれています。

- 最初の条件ステートメントでは、入力が検証されます。

- 2 番目のステートメントでは、 **[Add New Book]\(新しい書籍の追加\)** ユーザー インターフェイス (UI) セクションでユーザーが入力した文字列値から新しい <xref:System.Xml.Linq.XElement> が作成されます。

- 最後のステートメントでは、この新しい書籍要素が、L2DBForm.xaml のデータ プロバイダーに追加されます。 その結果、動的なデータ バインドによって UI がこの新しい項目で自動的に更新されます。ユーザーがコードを追加する必要はありません。

## <a name="onremove-event-handler"></a>OnRemove イベント ハンドラー
 `OnRemove` ハンドラーは、2 つの理由で `OnAddBook` ハンドラーよりも複雑です。 1 つは、生の XML に保持された空白が含まれているために、一致する改行を書籍エントリと共に削除する必要があることです。 もう 1 つは、削除された項目に設定されていた選択が、便宜上、一覧の前の項目にリセットされることです。

 ただし、選択された書籍項目を削除するための中心的な作業は、2 つのステートメントだけで完了します。

- まず、リスト ボックスで現在選択されている項目に関連する書籍要素が取得されます。

  ```
  XElement selBook = (XElement)lbBooks.SelectedItem;
  ```

- 次に、この要素がデータ プロバイダーから削除されます。

  ```
  selBook.Remove();
  ```

  この場合も、動的なデータ バインドによってプログラムの UI が自動的に更新されます。

## <a name="example"></a>例

### <a name="description"></a>説明

### <a name="code"></a>コード

```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Input;
using System.Xml;
using System.Xml.Linq;

namespace LinqToXmlDataBinding {
    /// <summary>
    /// Interaction logic for L2XDBForm.xaml
    /// </summary>

    public partial class L2XDBForm : System.Windows.Window
    {
        XNamespace mybooks = "http://www.mybooks.com";
        XElement bookList;

        public L2XDBForm()
        {
            InitializeComponent();
            bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
        }

        void OnRemoveBook(object sender, EventArgs e)
        {
            int index = lbBooks.SelectedIndex;
            if (index < 0) return;

            XElement selBook = (XElement)lbBooks.SelectedItem;
            //Get next node before removing element.
            XNode nextNode = selBook.NextNode;
            selBook.Remove();

            //Remove any matching newline node.
            if (nextNode != null && nextNode.ToString().Trim().Equals(""))
            { nextNode.Remove(); }

            //Set selected item.
            if (lbBooks.Items.Count > 0)
            {  lbBooks.SelectedItem = lbBooks.Items[index > 0 ? index - 1 : 0]; }
        }

        void OnAddBook(object sender, EventArgs e)
        {
            if (String.IsNullOrEmpty(tbAddID.Text) ||
                String.IsNullOrEmpty(tbAddValue.Text))
            {
                MessageBox.Show("Please supply both a Book ID and a Value!", "Entry Error!");
                return;
            }
            XElement newBook = new XElement(
                                mybooks + "book",
                                new XAttribute("id", tbAddID.Text),
                                tbAddValue.Text);
            bookList.Add("  ", newBook, "\r\n");
        }
    }
}

```

### <a name="comments"></a>コメント
 これらのハンドラーに関連する XAML ソースについては、「[L2DBForm.xaml ソース コード](../designers/l2dbform-xaml-source-code.md)」を参照してください。

## <a name="see-also"></a>参照
 [チュートリアル: LinqToXmlDataBinding Example](../designers/walkthrough-linqtoxmldatabinding-example.md) [l2dbform.xaml ソースコード](../designers/l2dbform-xaml-source-code.md)
