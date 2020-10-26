---
title: '方法: XML ファイルを編集する'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 02f078d9293fa8b02267c5003a92d1d60134e1a4
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88249516"
---
# <a name="how-to-edit-xml-files"></a>方法: XML ファイルを編集する

XML エディターは、XML ファイル用の新しいエディターです。 スタンドアロンの XML ファイル、または Visual Studio プロジェクトと関連付けられたファイルに対して使用できます。 XML エディターと関連付けられるファイル拡張子は、 *.config*、 *.dtd*、 *.xml*、 *.xsd*、 *.xdr*、 *.xs*l、 *.xslt*、および *.vssettings* です。 XML エディターは、特定のエディターが登録されておらず、XML や DTD のコンテンツを含む他のファイルの種類にも関連付けられます。

> [!NOTE]
> XHTML ドキュメントは HTML エディターによって処理されます。

XML ファイルを編集するには、編集するファイルを開きます。

## <a name="add-a-new-xml-file-to-a-project"></a>新しい XML ファイルをプロジェクトに追加する

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[テンプレート]** ペインの **[XML ファイル]** を選択します。

3. **[名前]** フィールドにファイル名を入力し、 **[追加]** をクリックします。

   XML ファイルがプロジェクトに追加され、XML エディターによって開かれます。 ファイルには既定の XML 宣言 `<?xml version="1.0" encoding="utf-8" ?>` が含まれています。

## <a name="add-an-existing-xml-file-to-a-project"></a>既存の XML ファイルをプロジェクトに追加する

1. **[プロジェクト]** メニューの **[既存項目の追加]** を選択します。

   **[既存項目の追加]** ダイアログ ボックスが表示されます。

2. XML ファイルを選択し、 **[追加]** をクリックします。

## <a name="create-a-new-xml-or-xslt-file"></a>新しい XML ファイルまたは XSLT ファイルを作成する

1. **[ファイル]** メニューの **[新規]** を選択します。

   **[新しいファイル]** ダイアログ ボックスが表示されます。

2. **[XML ファイル]** を選択して新しい XML ファイルを作成するか、 **[XSLT ファイル]** を選択して新しい XSLT スタイル シートを作成します。

3. **[Open (開く)]** を選択します。

## <a name="create-an-empty-project-for-xml-files"></a>XML ファイル用の空のプロジェクトを作成する

::: moniker range="vs-2017"

1. **[ファイル]** メニューで、 **[新規作成]** > **[プロジェクト]** の順に選択します。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. 任意のコード言語を選択し、 **[空のプロジェクト (.NET Framework)]** テンプレートを選択します。

3. **[OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. **[ファイル]** メニューで、 **[新規作成]** > **[プロジェクト]** の順に選択します。

2. テンプレート検索ボックスに「**空のプロジェクト**」と入力し、 **[空のプロジェクト (.NET Framework)]** テンプレートを選択して、 **[次へ]** を選択します。

3. **［作成］** を選択します

::: moniker-end

4. プロジェクトに XML ファイルを追加します。

   このプロジェクトに追加したスキーマは XML エディターによって検出され、このプロジェクトが開かれている間に編集する XML、スキーマ、または XSLT ファイルにおいて、検証と IntelliSense のために使用されます。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
- [XML ドキュメント プロパティと [プロパティ] ウィンドウ](../xml-tools/xml-document-properties-properties-window.md)
- [方法: XML ドキュメントから XML スキーマを作成する](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)
