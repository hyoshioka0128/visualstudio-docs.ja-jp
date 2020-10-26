---
title: 'チュートリアル: XML エディター機能の使用 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ea8dc357-2e66-455a-aec2-7ccaccfc9adf
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fa954cfb356593a4f22a44faddd69acdcfc93e37
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669569"
---
# <a name="walkthrough-using-xml-editor-features"></a>チュートリアル: XML エディター機能の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルの手順では、新しい XML ドキュメントを作成する方法を示します。 ここでは、XML の作成に役立つ XML エディターの機能もいくつか使用します。

> [!NOTE]
> このチュートリアルを開始する前に、hireDate.xsd ファイル (このトピックの最後に記載されています) をローカル コンピューターに保存してください。

### <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>新しい XML ファイルを作成して XML スキーマに関連付けるには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。

2. **[テンプレート]** ペインの **[XML ファイル]** をクリックし、 **[開く]** をクリックします。

     エディターに新しいファイルが開きます。 ファイルには既定の XML 宣言 `<?xml version="1.0" encoding="utf-8">` が含まれています。

3. ドキュメントのプロパティ ウィンドウで、 **[スキーマ]** フィールドの参照ボタン ( **[...]** ) をクリックします。

     **[XSD スキーマ]** ダイアログ ボックスが表示されます。

4. **[追加]** をクリックします。

     **[XSD スキーマを開く]** ダイアログ ボックスが表示されます。

5. hireDate.xsd ファイルを選択し、 **[開く]** をクリックします。

6. **[OK]** をクリックします。

     これで XML スキーマが XML ドキュメントと関連付けられます。 この XML スキーマは、ドキュメントの検証に使用されます。 有効な要素のメンバーの一覧を作成する際に、IntelliSense でも使用されます。

### <a name="to-add-data"></a>データを追加するには

1. エディターのペインに「`<`」と入力します。

     メンバーの一覧に使用可能な項目が表示されます。

    - **!--** はコメントを追加します。

    - **!DOCTYPE** はドキュメント型を追加します。

    - **?** は処理命令を追加します。

    - **employee** はルート要素を追加します。

2. [ ** \< !--** ] を選択してコメントノードを追加し、enter キーを押します。

     エディターによってコメントの終了タグが挿入され、コメントの開始タグと終了タグの間にカーソルが置かれます。

3. 「**Test XML file**」と入力します。

4. 新しい行に「`<`」と入力し、メンバーの一覧から **[employee]** を選択します。

     エディターにより、XML 要素の開始部分として `<employee` が追加されます。 この時点で、要素に属性を追加するか、「`>`」と入力して開始タグを閉じることができます。

5. 「`>`」と入力してタグを閉じます。

6. エディターによって終了タグが追加されます。 終了タグは、検証エラーを示す波下線付きで追加されます。 ツール ヒントには、次のメッセージが表示されます。"要素 'employee' に不完全な内容が含まれています。 'ID' を指定してください。"

7. 「`<`」と入力し、メンバーの一覧から **[ID]** を選択します。 次に、「`>`」と入力します。

     エディターには XML 要素 `<ID></ID>` が追加され、ID 開始タグの後にカーソルが置かれます。

8. 「**abc**」と入力します。

     「**abc**」というテキストに波下線が表示されます。 ツール ヒントには、次のメッセージが表示されます。"'ID' 要素はデータ型に対して無効な値です。"

9. ID 要素を右クリックし、[ **定義へのジャンプ**] を選択します。

     新しいドキュメント ウィンドウで hireDate.xsd ファイルが開かれ、ID の schema 要素定義の上にカーソルが置かれます。

10. XML ファイルに戻り、**abc** というテキストを **123** で置き換えます。

     ID 要素の値の下にあった波下線とツール ヒントが消去されます。 今度は、employee 終了タグのツール ヒントに次のメッセージが表示されます。"要素 'employee' に不完全な内容が含まれています。 'hire-date' を指定してください。"

11. ID 終了タグの後にカーソルを置き、「`<`」を入力します。メンバーの一覧から hire-date を選択し、「`>`」と入力します。

     エディターには XML 要素 `<hire-date></hire-date>` が追加され、hire-date 開始タグの後にカーソルが置かれます。

12. hire-date の値として「**2003-01-10**」と入力します。

### <a name="to-format-the-xml-document"></a>XML ドキュメントに書式を設定するには

1. XML エディターのツールバーから [ **ドキュメントの書式設定** ] ボタンを選択します。

     XML ドキュメントの書式が再設定されます。

### <a name="to-save-the-xml-document"></a>XML ドキュメントを保存するには

1. **[ファイル]** メニューから **[名前を付けて保存]** を選択します。

     **[名前を付けてファイルを保存]** ダイアログ ボックスが表示されます。 既定のファイル名は "XMLFile1" です。

2. この XML ドキュメントのファイル名と場所を入力し、 **[保存]** をクリックします。

## <a name="hiredatexsd-file"></a>hireDate.xsd ファイル
 このチュートリアルでは、次のスキーマ ファイルを使用します。

```
<?xml version="1.0"?>
<xs:schema attributeFormDefault="unqualified"
     elementFormDefault="qualified" targetNamespace="urn:empl-hire"
     xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="employee">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="ID" type="xs:unsignedShort" />
        <xs:element name="hire-date" type="xs:date" />
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## <a name="see-also"></a>参照
 [XML エディター](../xml-tools/xml-editor.md)
