---
title: '方法: Visual Studio 内で Word 文書にスキーマを割り当てる'
description: Visual Studio でドキュメントを開いているときに、XML スキーマを Microsoft Office Word 文書にマップする方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Word documents
- Word [Office development in Visual Studio], mapping XML schemas
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 082d5fe4fbcc7f66709770c16d3c9a1a2811e60d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900925"
---
# <a name="how-to-map-schemas-to-word-documents-inside-visual-studio"></a>方法: Visual Studio 内で Word 文書にスキーマを割り当てる
  **重要** このトピックに記載されている Microsoft Word に関する情報は、microsoft word のカスタム XML に関連する特定の機能の実装が microsoft によって削除されたときに、マイクロソフトが2010年1月より前にマイクロソフトによってライセンスされた Microsoft Word 製品米国の特典と使用についてのみ提供されます。 Microsoft Word に関するこの情報は、マイクロソフトが2010年1月10日以降にライセンスを取得した microsoft Word 製品を使用しているか、microsoft Word 製品で実行されているプログラムを開発している個人または米国組織によって読み取られたり使用されたりすることはできません。これらの製品は、その日より前にライセンスされている製品と同じように動作しないか、米国の外部で使用するために購入およびライセンス供与されます。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 ドキュメントが Visual Studio で開かれているときに、XML スキーマをドキュメントにマップできます。 Visual Studio の外部でドキュメントを開くときに使用するのと同じ Microsoft Office Word ツールを使用します。 Word ソリューションを作成する前または後に、ドキュメントにスキーマをマップするかどうかにかかわらず、Office プロジェクトによって同じオブジェクトが作成されます。

## <a name="to-map-an-xml-schema-to-a-word-document-in-visual-studio"></a>Visual Studio で XML スキーマを Word 文書にマップするには

1. Visual Studio 内で Word 文書またはテンプレートプロジェクトを開きます。

2. ドキュメント内をクリックして、デザイナーにフォーカスを移動します。

3. リボンの [ **開発者** ] タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「 [方法: リボンに [開発者] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

4. [ **XML** ] グループの [ **スキーマ**] をクリックします。

     [ **テンプレートとアドイン** ] ダイアログボックスが表示されます。

5. [ **XML スキーマ** ] タブをクリックします。

6. [ **スキーマの追加**] をクリックします。

     [ **スキーマの追加** ] ダイアログボックスが表示されます。

7. スキーマファイルを参照して選択し、[ **開く**] をクリックします。

     [ **スキーマの設定** ] ダイアログボックスが表示されます。

8. 別名を割り当てます。または、[ **OK** ] をクリックしてエイリアスを指定せずにスキーマを追加します。

9. **[OK]** をクリックします。

     [ **XML 構造** ] ウィンドウが開きます。

10. **XML 構造** ウィンドウから、対応するコントロールを作成するドキュメント内の場所に要素をドラッグします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio 内のワークシートにスキーマをマップする](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [ドキュメントレベルのカスタマイズにおける XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
