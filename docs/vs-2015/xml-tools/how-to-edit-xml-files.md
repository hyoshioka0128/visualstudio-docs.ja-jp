---
title: '方法: XML ファイルを編集する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c099839cda87819ec0ec7932c2b2e6aa7698fa52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670885"
---
# <a name="how-to-edit-xml-files"></a>方法: XML ファイルを編集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML エディターは、XML ファイル用の新しいエディターです。 スタンドアロンの XML ファイル、または Visual Studio プロジェクトと関連付けられたファイルに対して使用できます。 XML エディターと関連付けられるファイル拡張子は、.config、.dtd、.xml、.xsd、.xdr、.xsl、.xslt、および .vssettings です。 XML エディターは、特定のエディターが登録されておらず、XML や DTD のコンテンツを含む他のファイルの種類にも関連付けられます。

> [!NOTE]
> XHTML ドキュメントは HTML エディターによって処理されます。

### <a name="to-edit-an-xml-file"></a>XML ファイルを編集するには

1. 編集するファイルをダブルクリックします。

### <a name="to-add-a-new-xml-file-to-a-project"></a>新しい XML ファイルをプロジェクトに追加するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[テンプレート]** ペインの **[XML ファイル]** を選択します。

3. **[名前]** フィールドにファイル名を入力し、 **[追加]** をクリックします。

     XML ファイルがプロジェクトに追加され、XML エディターによって開かれます。 ファイルには既定の XML 宣言 `<?xml version="1.0" encoding="utf-8" ?>` が含まれています。

### <a name="to-add-an-existing-xml-file-to-a-project"></a>既存の XML ファイルをプロジェクトに追加するには

1. **[プロジェクト]** メニューの **[既存項目の追加]** を選択します。

     **[既存項目の追加]** ダイアログ ボックスが表示されます。

2. XML ファイルを選択し、 **[追加]** をクリックします。

### <a name="to-create-a-new-xml-or-xslt-file"></a>新しい XML ファイルまたは XSLT ファイルを作成するには

1. **[ファイル]** メニューの **[新規]** を選択します。

     **[新しいファイル]** ダイアログ ボックスが表示されます。

2. **[XML ファイル]** を選択して新しい XML ファイルを作成するか、 **[XSLT ファイル]** を選択して新しい XSLT スタイル シートを作成します。

3. **[開く]** をクリックします。

### <a name="to-create-a-project-for-xml-files"></a>XML ファイル用のプロジェクトを作成するには

1. **[ファイル]** メニューの **[新規作成]** を選択し、**[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. 任意のコード言語を選択し、[ **空のプロジェクト**] を選択して、[ **OK**] をクリックします。

3. プロジェクトに XML ファイルを追加します。

     このプロジェクトに追加したスキーマは XML エディターによって検出され、このプロジェクトが開かれている間に編集する XML、スキーマ、または XSLT ファイルにおいて、検証と IntelliSense のために使用されます。

## <a name="see-also"></a>参照
 Xml[エディター](../xml-tools/xml-editor.md) [の Xml ドキュメントのプロパティ [プロパティ] ウィンドウ](../xml-tools/xml-document-properties-properties-window.md)[方法: xml ドキュメントから xml スキーマを作成する](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)
