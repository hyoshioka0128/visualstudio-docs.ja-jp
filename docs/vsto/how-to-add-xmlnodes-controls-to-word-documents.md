---
title: '方法: Word 文書に XMLNodes コントロールを追加する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, adding to documents
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 95fc165c1a3123d68529f6ccaea99fea963c2a67
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543495"
---
# <a name="how-to-add-xmlnodes-controls-to-word-documents"></a>方法: Word 文書に XMLNodes コントロールを追加する
  **重要**このトピックに記載されている Microsoft Word に関する情報は、microsoft word のカスタム XML に関連する特定の機能の実装が microsoft によって削除されたときに、マイクロソフトが2010年1月より前にマイクロソフトによってライセンスされた Microsoft Word 製品米国の特典と使用についてのみ提供されます。 Microsoft Word に関するこの情報は、マイクロソフトが2010年1月10日以降にライセンスを取得した microsoft Word 製品を使用しているか、microsoft Word 製品で実行されているプログラムを開発している個人または米国組織によって読み取られたり使用されたりすることはできません。これらの製品は、その日より前にライセンスされている製品と同じように動作しないか、米国の外部で使用するために購入およびライセンス供与されます。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 繰り返し XML スキーマ要素を Microsoft Office Word 文書にマップすると、Visual Studio に <xref:Microsoft.Office.Tools.Word.XMLNodes> よって自動的にコントロールがドキュメントに追加されます。

 非繰り返し XML スキーマ要素のマッピングの詳細については、「[方法: Word 文書に XMLNode コントロールを追加](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)する」を参照してください。

> [!NOTE]
> コントロールは、 <xref:Microsoft.Office.Tools.Word.XMLNodes> **ツールボックス**または [**データソース**] ウィンドウからは使用できません。また、プログラムによって作成することもできません。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-an-xmlnodes-control-to-a-document"></a>XMLNodes コントロールをドキュメントに追加するには

1. Visual Studio デザイナーのドキュメントのリボンで、[**開発者**] タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: リボンに [開発者] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

2. [ **XML** ] グループの [**スキーマ**] をクリックします。

     [**テンプレートとアドイン**] ダイアログボックスが表示されます。

3. [ **XML スキーマ**] タブをクリックします。

4. [**スキーマの追加**] をクリックします。

     [**スキーマの追加**] ダイアログボックスが表示されます。

5. 繰り返しスキーマ要素を含む XML スキーマを選択し、[**開く**] をクリックします。

     [**スキーマの設定**] ダイアログボックスが表示されます。

6. 別名を割り当てます。または、[ **OK** ] をクリックしてエイリアスを指定せずにスキーマを追加します。

     [**スキーマの追加**] ダイアログボックスにスキーマが追加されます。

7. [**スキーマの追加**] ダイアログボックスで、[ **OK]** をクリックします。

     [ **XML 構造**] 作業ウィンドウが開きます。

8. [ **XML 構造**] 作業ウィンドウで [繰り返しスキーマ] 要素をクリックして、ドキュメントに追加します。

     <xref:Microsoft.Office.Tools.Word.XMLNodes>コントロールが作成され、プロジェクトに追加されます。

## <a name="see-also"></a>関連項目
- [XMLNodes コントロール](../vsto/xmlnodes-control.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
