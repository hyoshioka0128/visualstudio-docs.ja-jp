---
title: 'チュートリアル: XML エディター機能の使用'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ea8dc357-2e66-455a-aec2-7ccaccfc9adf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d2cf35730b70fc8c8bbec392c73b444b6e8e0aaa
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592465"
---
# <a name="walkthrough-use-xml-editor-features"></a>チュートリアル: XML エディター機能の使用

このチュートリアルの手順では、新しい XML ドキュメントを作成する方法を示します。 このチュートリアルでは、xml エディターの機能の一部も使用しており、XML の作成に役立ちます。

> [!NOTE]
> チュートリアルを開始する前に、 *hireDate*ファイル (このトピックで後述します) をローカルコンピューターに保存します。

## <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>新しい XML ファイルを作成して XML スキーマに関連付けるには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。

2. **[テンプレート]** ペインで **[XML ファイル]** を選択し、 **[開く]** をクリックします。

     エディターに新しいファイルが開きます。 ファイルには既定の XML 宣言 `<?xml version="1.0" encoding="utf-8">` が含まれています。

3. ドキュメントのプロパティ ウィンドウで、参照 ボタンをクリックします ( **...** ) で、**スキーマ**フィールド。

     **[XSD スキーマ]** ダイアログボックスが表示されます。

4. **[追加]** をクリックします。

     **[XSD スキーマを開く]** ダイアログボックスが表示されます。

5. *HireDate*ファイルを選択し、 **[開く]** をクリックします。

6. **[OK]** をクリックします。

     これで XML スキーマが XML ドキュメントと関連付けられます。 この XML スキーマは、ドキュメントの検証に使用されます。 有効な要素のメンバーの一覧を作成する際に、IntelliSense でも使用されます。

## <a name="to-add-data"></a>データを追加するには

1. エディターのペインに「`<`」と入力します。

     メンバーの一覧に使用可能な項目が表示されます。

    - コメントを追加する **!--** ます。

    - **!DOCTYPE** 。ドキュメントの種類を追加します。

    - **?** 処理命令を追加する場合は。

    - ルート要素を追加する**従業員**。

2. **&lt;!--** を選択してコメントノードを追加し **、enter キーを押します**。

     エディターによってコメントの終了タグが挿入され、コメントの開始タグと終了タグの間にカーソルが置かれます。

3. **テスト XML ファイル**に「」と入力します。

4. 新しい行に「`<`」と入力し、メンバーの一覧から **[employee]** を選択します。

     エディターにより、XML 要素の開始部分として `<employee` が追加されます。 この時点で、要素に属性を追加するか、「`>`」と入力して開始タグを閉じることができます。

5. 「`>`」と入力してタグを閉じます。

6. エディターによって終了タグが追加されます。 終了タグは、検証エラーを示す波下線付きで追加されます。 **ツールヒント**にメッセージが表示されます。**要素 ' employee ' に不完全な内容が含まれています。' ID ' が必要**です。

7. 「`<`」と入力し、メンバー ボックスの一覧から  **ID** を選択します。 次に、「`>`」と入力します。

     エディターには XML 要素 `<ID></ID>` が追加され、ID 開始タグの後にカーソルが置かれます。

8. 「 **Abc**」と入力します。

     **Abc**テキストに波下線が表示されます。 **ツールヒント**にメッセージが表示されます。 **' ID ' 要素のデータ型に対して無効な値が指定**されています。

9. ID 要素を右クリックし、 **[定義へのジャンプ]** を選択します。

     エディターによって、新しいドキュメントウィンドウに*hireDate*ファイルが開き、ID スキーマ要素の定義にカーソルが配置されます。

10. XML ファイルに戻り、 **abc**テキストを**123**に置き換えます。

     ID 要素の値の下に波線と**ツールヒント**がクリアされます。 Employee end タグの**ツールヒント**に、 **"要素 ' employee ' に不完全な内容が含まれています" というメッセージが表示されるようになりました。' 入社日 ' が必要**です。

11. ID 終了タグの後にカーソルを置き、`<`に「」と入力し、メンバーリストから **[入社日]** を選択して、「`>`」と入力します。

     エディターには XML 要素 `<hire-date></hire-date>` が追加され、hire-date 開始タグの後にカーソルが置かれます。

12. 入社日の値として「 **2003-01-10** 」と入力します。

## <a name="to-format-the-xml-document"></a>XML ドキュメントに書式を設定するには

- XML エディター ツールバーの **ドキュメントの書式設定** ボタンを選択するか、 **ctrl**+**E**、**D**キーを押します。

   ![Visual Studio の [XML ドキュメントの書式設定] ボタン](media/format-xml-document.png)

   XML ドキュメントの書式が再設定されます。

## <a name="to-save-the-xml-document"></a>XML ドキュメントを保存するには

1. **[ファイル]** メニューの **[名前を付けて保存]** を選択します。

     **[ファイル名を付けて保存]** ダイアログボックスが表示されます。 既定のファイル名は *' XMLFile1 '* です。

2. XML ドキュメントのファイル名と場所を入力し、 **[保存]** をクリックします。

## <a name="hiredatexsd-file"></a>hireDate ファイル

このチュートリアルでは、次のスキーマファイルを使用します。

```xml
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

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
