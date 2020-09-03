---
title: '方法: 使用する XML スキーマを選択する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: d6fda3ef-d465-4788-8514-2f2d528d658c
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f607d500bfcb8a745bfb129490d2c2b09c6b105c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72666508"
---
# <a name="how-to-select-the-xml-schemas-to-use"></a>方法: 使用する XML スキーマを選択する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML エディターはスキーマ キャッシュを提供します。このキャッシュは %InstallDir%\Xml\Schemas ディレクトリに配置されています。 スキーマ キャッシュには、IntelliSense と XML ドキュメントの検証に使用される既知の XML スキーマが格納されています。

 **スキーマ**ドキュメントプロパティは、使用する1つ以上の XML スキーマ定義言語 (XSD) スキーマを選択するために使用されます。 このプロパティによって、スキーマ キャッシュにあるスキーマの選択、またはキャッシュ内に置かれていないスキーマの指定が可能になります。

 指定したスキーマは、他のすべての XML ドキュメント プロパティと共に非表示のソリューション ユーザー オプション ファイル (.suo) に保存されます。 このため、ソリューションを次に開いたときにプロパティの値を再入力する必要はありません。

> [!NOTE]
> エディターは、インライン スキーマ、または `xsd:schemaLocation` 属性によって参照されているスキーマを使用して検証を行うことができます。 詳細については、「 [XML ドキュメントの検証](../xml-tools/xml-document-validation.md)」を参照してください。

### <a name="to-select-an-xml-schema-from-the-schema-cache"></a>スキーマ キャッシュにある XML スキーマを選択するには

1. XML エディターでファイルを開きます。

2. ドキュメントのプロパティ ウィンドウで、 **[スキーマ]** フィールドのボタンをクリックします。

    [ **XML スキーマ** ] ダイアログボックスが表示されます。 このダイアログボックスには、スキーマキャッシュ内の .xsd 拡張子を持つすべてのスキーマ (catalog.xml ファイルで参照されるスキーマを含む) と、現在のソリューション内のスキーマ、Visual Studio で開く、属性で参照されるスキーマ、 `xsd:schemaLocation` また**Schemas**は schema プロパティで参照されるスキーマがすべて一覧表示されます。

3. 次のいずれかを実行し、検証に使用するスキーマを選択します。

   - **[XML スキーマ]** ダイアログに一覧表示されるスキーマを 1 つ選択し、 **[使用]** 列をクリックして、 **[このスキーマを使用する]** をクリックします。

     \- または -

   - [ **XML スキーマ** ] ダイアログボックスに表示されている複数のスキーマを選択し、右クリックして、[ **このスキーマを使用する**] を選択します。

4. **[OK]** をクリックします。

    選択したスキーマの一覧が **[スキーマ]** ドキュメント プロパティにコピーされます。

### <a name="to-add-an-xml-schema-to-the-schema-cache"></a>XML スキーマをスキーマ キャッシュに追加するには

1. ドキュメントのプロパティ ウィンドウで、 **[スキーマ]** フィールドのボタンをクリックします。

2. **[追加]** をクリックします。

     [ **XSD スキーマを開く** ] ダイアログボックスが開きます。

3. スキーマ キャッシュに追加するスキーマを参照し、選択します。

4. **[開く]** をクリックします。

     スキーマがスキーマキャッシュに追加され、[ **使用** ] 列の値が [ **このスキーマを使用**する] に設定されています。

### <a name="to-delete-an-xml-schema-from-the-schema-cache"></a>スキーマ キャッシュにある XML スキーマを削除するには

1. ドキュメントのプロパティ ウィンドウで、 **[スキーマ]** フィールドのボタンをクリックします。

2. 削除するスキーマを選択し、 **[削除]** をクリックします。

     スキーマは、メモリ内のスキーマ キャッシュから削除されますが、ファイル システムからは削除されません。

    > [!NOTE]
    > `schemaLocation` 属性または一致する `targetNamespace` を介したスキーマへの参照がまだ存在する場合、 **[削除]** は、自動的な関連付けによりこの状況では機能しません。 この場合は、スキーマを **[使用]** 列の **[選択されているスキーマを使用しない]** としてマークすることをお勧めします。

## <a name="see-also"></a>参照
 [[スキーマキャッシュ](../xml-tools/schema-cache.md) [Xml スキーマ] ダイアログボックス](../xml-tools/xml-schemas-dialog-box.md) [xml エディター](../xml-tools/xml-editor.md)
