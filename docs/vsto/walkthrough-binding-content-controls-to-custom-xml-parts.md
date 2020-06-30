---
title: 'チュートリアル: カスタム XML 部分へのコンテンツコントロールのバインド'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PlainTextContentControl, binding to a custom XML part
- custom XML parts, binding to content controls
- content controls [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], content controls
- DropDownListContentControl, binding items to a custom XML part
- DatePickerContentControl, binding to a custom XML part
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a80488408f680530ed3c9b4094b2997e97484ce3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544444"
---
# <a name="walkthrough-bind-content-controls-to-custom-xml-parts"></a>チュートリアル: カスタム XML 部分へのコンテンツコントロールのバインド
  このチュートリアルでは、Word のドキュメント レベルのカスタマイズで、コンテンツ コントロールを同じ文書内の XML データにバインドする方法を説明します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Word を使用すると、*カスタム xml 部分*という名前の xml データをドキュメントに格納できます。 このデータの表示は、カスタム XML 部分の要素にコンテンツ コントロールをバインドすることによって制御できます。 このチュートリアルで例として示す文書のカスタム XML 部分には、従業員情報が格納されています。 この文書を開くと、XML 要素の値がコンテンツ コントロールに表示されます。 コンテンツ コントロール内のテキストに加えた変更は、カスタム XML 部分に保存されます。

 このチュートリアルでは、次の作業について説明します。

- デザイン時におけるドキュメント レベルのプロジェクトの Word 文書へのコンテンツ コントロールの追加

- XML データ ファイルと、コンテンツ コントロールにバインドする要素を定義する XML スキーマを作成する。

- デザイン時に XML スキーマを文書に添付する。

- 実行時に XML ファイルの内容を文書内のカスタム XML 部分に追加する。

- コンテンツ コントロールをカスタム XML 部分の要素にバインドする。

- <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を XML スキーマに定義された値にバインドする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-a-new-word-document-project"></a>新しい Word 文書プロジェクトを作成する
 このチュートリアルで使用する Word 文書を作成します。

### <a name="to-create-a-new-word-document-project"></a>Word 文書プロジェクトを作成するには

1. **Employeecontrols.docx**という名前の Word 文書プロジェクトを作成します。 ソリューションの新しい文書を作成します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]デザイナーで新しい Word 文書を開き、**ソリューションエクスプローラー**に**employeecontrols.docx**プロジェクトを追加します。

## <a name="add-content-controls-to-the-document"></a>ドキュメントにコンテンツコントロールを追加する
 ユーザーが従業員に関する情報を表示または編集できる 3 種類のコンテンツ コントロールが含まれるテーブルを作成します。

### <a name="to-add-content-controls-to-the-document"></a>文書にコンテンツ コントロールを追加するには

1. デザイナーでホストされている Word 文書で、リボンの [ [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **挿入**] タブを選択します。

2. [**テーブル**] グループで、[**テーブル**] を選択し、2つの列と3つの行を含むテーブルを挿入します。

3. 最初の列に次のようにテキストを入力します。

   ||
   |-|
   |**Employee Name**|
   |**Hire Date**|
   |**Title**|

4. テーブルの2番目の列で、最初の行 ([ **Employee Name**] の横) を選択します。

5. リボンの [**開発者**] タブをクリックします。

   > [!NOTE]
   > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: リボンに [開発者] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

6. [**コントロール**] グループの [**テキスト**] ボタン![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl")をクリックして、 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 最初のセルにを追加します。

7. テーブルの2番目の列で、2番目の行 ([**入社日**] の横) を選択します。

8. [**コントロール**] グループの [**日付の選択**] ボタン![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl")をクリックして、 <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> 2 番目のセルにを追加します。

9. テーブルの2番目の列で、3番目の行 ([**タイトル**] の横) を選択します。

10. [**コントロール**] グループで、**ドロップダウンリスト**の [ ![dropdownlistcontentcontrol](../vsto/media/dropdownlist.gif "DropDownListContentControl") ] を選択して、最後のセルにを追加し <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> ます。

    これで、このプロジェクトのユーザー インターフェイスが完成しました。 ここでこのプロジェクトを実行すると、最初の行にテキストを入力し、2 つ目の行で日付を選択できます。 次の手順では、表示するデータを XML ファイル内の文書に添付します。

## <a name="create-the-xml-data-file"></a>XML データファイルの作成
 通常は、ファイルやデータベースなどの外部ソースからカスタム XML 部分に格納する XML 文字列を取得する必要があります。 このチュートリアルでは、文書内のコンテンツ コントロールにバインドする要素でマークされた従業員データを含む、XML ファイルを作成します。 データを実行時に使用できるようにするには、XML ファイルをリソースとしてカスタマイズアセンブリに埋め込みます。

#### <a name="to-create-the-data-file"></a>データ ファイルを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. [**テンプレート**] ペインで、[ **XML ファイル**] を選択します。

3. ファイルに**employees.xml**という名前を指定し、[**追加**] ボタンをクリックします。

     コードエディターで**employees.xml**ファイルが開きます。

4. **employees.xml**ファイルの内容を次のテキストに置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <employees xmlns="http://schemas.microsoft.com/vsto/samples">
      <employee>
        <name>Karina Leal</name>
        <hireDate>1999-04-01</hireDate>
        <title>Manager</title>
      </employee>
    </employees>
    ```

5. **ソリューションエクスプローラー**で、 **employees.xml**ファイルを選択します。

6. [**プロパティ**] ウィンドウで、[**ビルドアクション**] プロパティを選択し、値を [**埋め込みリソース**] に変更します。

     この操作によって、プロジェクトをビルドしたときに、XML ファイルがリソースとしてアセンブリに埋め込まれます。 これにより、実行時に XML ファイルの内容にアクセスできます。

## <a name="create-an-xml-schema"></a>XML スキーマを作成する
 コンテンツ コントロールをカスタム XML 部分の 1 つの要素にバインドする場合は、XML スキーマを使用する必要はありません。 ただし、<xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を複数の値にバインドする場合は、前の手順で作成した XML データ ファイルを検証する XML スキーマを作成する必要があります。 XML スキーマには、`title` 要素に割り当てることができる値を定義します。 このチュートリアルの後半で、この要素に <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> をバインドします。

#### <a name="to-create-an-xml-schema"></a>XML スキーマを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. [**テンプレート**] ペインで、[ **XML スキーマ**] を選択します。

3. スキーマに「 **employees** 」という名前を指定し、[**追加**] ボタンをクリックします。

     スキーマ デザイナーが開きます。

4. **ソリューションエクスプローラー**で、 **employees**のショートカットメニューを開き、[**コードの表示**] を選択します。

5. **Employees**ファイルの内容を次のスキーマに置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <xs:schema xmlns="http://schemas.microsoft.com/vsto/samples"
        targetNamespace="http://schemas.microsoft.com/vsto/samples"
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        elementFormDefault="qualified">
      <xs:element name="employees" type="EmployeesType"></xs:element>
      <xs:complexType name="EmployeesType">
        <xs:all>
          <xs:element name="employee" type="EmployeeType"/>
        </xs:all>
      </xs:complexType>
      <xs:complexType name="EmployeeType">
        <xs:sequence>
          <xs:element name="name" type="xs:string" minOccurs="1" maxOccurs="1"/>
          <xs:element name="hireDate" type="xs:date" minOccurs="1" maxOccurs="1"/>
          <xs:element name="title" type="TitleType" minOccurs="1" maxOccurs="1"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="TitleType">
        <xs:restriction base="xs:string">
          <xs:enumeration value ="Engineer"/>
          <xs:enumeration value ="Designer"/>
          <xs:enumeration value ="Manager"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:schema>
    ```

6. [**ファイル**] メニューの [**すべてを保存**] をクリックして、 **employees.xml**と**employees の .xsd**ファイルに対する変更を保存します。

## <a name="attach-the-xml-schema-to-the-document"></a>XML スキーマをドキュメントに添付する
 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を `title` 要素の有効な値にバインドするためには、XML スキーマを文書に添付する必要があります。

### <a name="to-attach-the-xml-schema-to-the-document--word_15_short"></a>XML スキーマをドキュメントに添付するには ( [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] )

1. デザイナーで**EmployeeControls.docx**をアクティブにします。

2. リボンで [**開発者**] タブを選択し、[**アドイン**] をクリックします。

3. [**テンプレートとアドイン**] ダイアログボックスで、[ **XML スキーマ**] タブを選択し、[**スキーマの追加**] をクリックします。

4. 前の手順で作成した、プロジェクトディレクトリにある、先ほど作成した**employees**スキーマを参照し、[**開く**] ボタンをクリックします。

5. [**スキーマの設定**] ダイアログボックスの **[OK** ] をクリックします。

6. **[OK** ] をクリックして、[**テンプレートとアドイン**] ダイアログボックスを閉じます。

### <a name="to-attach-the-xml-schema-to-the-document-word-2010"></a>XML スキーマをドキュメントに添付するには (Word 2010)

1. デザイナーで**EmployeeControls.docx**をアクティブにします。

2. リボンの [**開発者**] タブをクリックします。

3. [ **XML** ] グループの [**スキーマ**] ボタンをクリックします。

4. [**テンプレートとアドイン**] ダイアログボックスで、[ **XML スキーマ**] タブを選択し、[**スキーマの追加**] をクリックします。

5. 先ほど作成した、プロジェクトディレクトリにある、先ほど作成した**employees**スキーマを参照し、[**開く**] ボタンをクリックします。

6. [**スキーマの設定**] ダイアログボックスの **[OK** ] をクリックします。

7. **[OK** ] をクリックして、[**テンプレートとアドイン**] ダイアログボックスを閉じます。

     [ **XML 構造**] 作業ウィンドウが開きます。

8. [ **XML 構造**] 作業ウィンドウを閉じます。

## <a name="add-a-custom-xml-part-to-the-document"></a>カスタム XML 部分をドキュメントに追加する
 コンテンツ コントロールを XML ファイル内の要素にバインドするためには、XML ファイルの内容を文書内の新しいカスタム XML 部分に追加する必要があります。

### <a name="to-add-a-custom-xml-part-to-the-document"></a>カスタム XML 部分を文書に追加するには

1. **ソリューションエクスプローラー**で、 **ThisDocument.cs**または**ThisDocument**のショートカットメニューを開き、[コードの**表示**] を選択します。

2. `ThisDocument` クラスに次の宣言を追加します。 このコードでは、カスタム XML 部分を文書に追加するために使用する複数のオブジェクトを宣言しています。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#1)]

3. `ThisDocument` クラスに次のメソッドを追加します。 このメソッドは、アセンブリにリソースとして埋め込まれている XML データ ファイルの内容を取得し、それを XML 文字列として返します。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#3)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#3)]

4. `ThisDocument` クラスに次のメソッドを追加します。 `AddCustomXmlPart` メソッドは、受け取った XML 文字列を含むカスタム XML 部分を作成します。

     カスタム XML 部分が一度だけ作成されるように、このメソッドは、一致する GUID を持つカスタム XML 部分が文書内に存在しない場合のみカスタム XML 部分を作成します。 このメソッドは、初めて呼び出されたときに、<xref:Microsoft.Office.Core._CustomXMLPart.Id%2A> プロパティの値を `employeeXMLPartID` 文字列に格納します。 `employeeXMLPartID` 文字列の値は、<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性によって宣言されているため、文書内に保持されます。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#4)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#4)]

## <a name="bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>カスタム XML 部分の要素にコンテンツコントロールをバインドする
 各コンテンツコントロールの**Xmlmapping**プロパティを使用して、各コンテンツコントロールをカスタム XML 部分の要素にバインドします。

### <a name="to-bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>コンテンツ コントロールをカスタム XML 部分の要素にバインドするには

1. `ThisDocument` クラスに次のメソッドを追加します。 このメソッドは、各コンテンツ コントロールをカスタム XML 部分の要素にバインドし、<xref:Microsoft.Office.Tools.Word.DatePickerContentControl> の日付表示形式を設定します。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#5)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#5)]

## <a name="run-your-code-when-the-document-is-opened"></a>ドキュメントを開いたときにコードを実行する
 カスタム XML 部分を作成し、文書が開かれたときにカスタム コントロールをデータにバインドします。

### <a name="to-run-your-code-when-the-document-is-opened"></a>文書が開かれたときにコードを実行するには

1. `ThisDocument_Startup` クラスの `ThisDocument` メソッドに次のコード行を追加します。 このコードは、 **employees.xml**ファイルから xml 文字列を取得し、その xml 文字列をドキュメント内の新しいカスタム xml 部分に追加して、コンテンツコントロールをカスタム xml 部分の要素にバインドします。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#2)]

## <a name="test-the-project"></a>プロジェクトのテスト
 文書を開くと、コンテンツ コントロールにカスタム XML 部分の要素のデータが表示されます。 をクリックして、 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> `title` 従業員の **.xsd**ファイルで定義されている要素の3つの有効な値のいずれかを選択できます。 コンテンツ コントロールに表示されたデータを編集すると、新しい値が文書内のカスタム XML 部分に保存されます。

### <a name="to-test-the-content-controls"></a>コンテンツ コントロールをテストするには

1. **F5**キーを押してプロジェクトを実行します。

2. 文書内に次のようなテーブルが表示されることを確認します。 2 つ目の列の文字列は、文書内のカスタム XML 部分の要素から取得されます。

    |列|値|
    |-|-|
    |**Employee Name**|**Karina Leal**|
    |**Hire Date**|**April 1, 1999**|
    |**Title**|**マネージャー**|

3. [ **Employee name** ] セルの右側にあるセルを選択し、別の名前を入力します。

4. [**入社日**] セルの右側にあるセルを選択し、日付の選択で別の日付を選択します。

5. **タイトル**セルの右側にあるセルを選択し、ドロップダウンリストから新しい項目を選択します。

6. 文書を保存して閉じます。

7. ファイルエクスプローラーで、プロジェクトの場所の下にある [ *\bin\debug* ] フォルダーを開きます。

8. **EmployeeControls.docx**のショートカットメニューを開き、[**名前の変更**] を選択します。

9. ファイルに**EmployeeControls.docx.zip**という名前を指定します。

     **EmployeeControls.docx**ドキュメントは、Open XML 形式で保存されます。 このドキュメントの名前を *.zip*ファイル名拡張子に変更すると、ドキュメントの内容を確認できます。 Open XML の詳細については、技術記事「 [Office (2007) OPEN xml ファイル形式の概要](/previous-versions/office/developer/office-2007/aa338205(v=office.12))」を参照してください。

10. **EmployeeControls.docx.zip**ファイルを開きます。

11. **Customxml**フォルダーを開きます。

12. **item2.xml**のショートカットメニューを開き、[**開く**] を選択します。

     このファイルには、文書に追加したカスタム XML 部分が含まれています。

13. `name`、`hireDate`、`title` の各要素に文書内のコンテンツ コントロールに入力した値が設定されていることを確認します。

14. **item2.xml**ファイルを閉じます。

## <a name="next-steps"></a>次のステップ
 コンテンツ コントロールの使用方法の詳細については、次の各トピックを参照してください。

- 用意されているすべてのコンテンツ コントロールを使用してテンプレートを作成できます。 詳細については、「[チュートリアル: コンテンツコントロールを使用してテンプレートを作成する](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)」を参照してください。

- 文書を閉じた状態でカスタム XML 部分のデータを変更できます。 その文書を次にユーザーが開いたときには、XML 要素にバインドされたコンテンツ コントロールに新しいデータが表示されます。

- コンテンツ コントロールを使用して文書の一部を保護できます。 詳細については、「[方法: コンテンツコントロールを使用してドキュメントの一部を保護](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [コンテンツ コントロール](../vsto/content-controls.md)
- [方法: Word 文書にコンテンツコントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [方法: コンテンツコントロールを使用して文書の一部を保護する](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
