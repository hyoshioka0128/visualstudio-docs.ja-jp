---
title: '方法 : XML ファイルを編集する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 216718627936ac7f519c1a6a28a30886e8ae9c27
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592738"
---
# <a name="how-to-edit-xml-files"></a>方法: XML ファイルを編集する

Xml エディターは、XML ファイル用の新しいエディターです。 スタンドアロンの XML ファイル、または Visual Studio プロジェクトと関連付けられたファイルに対して使用できます。 XML エディターは、 *.config*、 *dtd*、 *.xml*、 *.xsd*、 *xdr*、 *.xsl*、 *.xslt*、および *.vssettings*の各ファイル拡張子に関連付けられています。 XML エディターは、特定のエディターが登録されておらず、XML または DTD コンテンツを含むその他のファイルの種類にも関連付けられています。

> [!NOTE]
> XHTML ドキュメントは HTML エディターによって処理されます。

XML ファイルを編集するには、編集するファイルをダブルクリックします。

## <a name="add-a-new-xml-file-to-a-project"></a>新しい XML ファイルをプロジェクトに追加する

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[テンプレート]** ペインで **[XML ファイル]** を選択します。

3. **[名前]** フィールドにファイル名を入力し、 **[追加]** をクリックします。

   XML ファイルがプロジェクトに追加され、XML エディターで開かれます。 ファイルには既定の XML 宣言 `<?xml version="1.0" encoding="utf-8" ?>` が含まれています。

## <a name="add-an-existing-xml-file-to-a-project"></a>既存の XML ファイルをプロジェクトに追加する

1. **[プロジェクト]** メニューの **[既存項目の追加]** を選択します。

   **[既存項目の追加]** ダイアログボックスが表示されます。

2. XML ファイルを選択し、 **[追加]** をクリックします。

## <a name="create-a-new-xml-or-xslt-file"></a>新しい XML ファイルまたは XSLT ファイルを作成します。

1. **[ファイル]** メニューの **[新規作成]** をクリックします。

   **[新しいファイル]** ダイアログ ボックスが表示されます。

2. 新しい XML ファイルを作成するには、 **[Xml ファイル]** を選択します。または、 **[Xslt ファイル]** を選択して新しい xslt スタイルシートを作成します。

3. **[開く]** をクリックします。

## <a name="create-an-empty-project-for-xml-files"></a>XML ファイルに空のプロジェクトを作成する

::: moniker range="vs-2017"

1. **[ファイル]** メニューの [**新しい**>**プロジェクト**] をクリックします。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. 任意のコード言語を選択し、 **[空のプロジェクト (.NET Framework)]** テンプレートを選択します。

3. **[OK]** をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. **[ファイル]** メニューの [**新しい**>**プロジェクト**] をクリックします。

2. テンプレート検索ボックスに**空のプロジェクト**を入力し、 **[空のプロジェクト (.NET Framework)]** テンプレートを選択して、 **[次へ]** をクリックします。

3. **[作成]** をクリックします。

::: moniker-end

4. プロジェクトに XML ファイルを追加します。

   XML エディターは、このプロジェクトに追加したスキーマを検索し、このプロジェクトが開いている間に編集する XML、スキーマ、または XSLT ファイルの検証と IntelliSense に使用します。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
- [[XML ドキュメントのプロパティ] ([プロパティ] ウィンドウ)](../xml-tools/xml-document-properties-properties-window.md)
- [方法: XML ドキュメントから XML スキーマを作成する](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)
