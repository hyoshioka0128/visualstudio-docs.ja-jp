---
title: カスタム XML 部分の概要
description: 一部の Microsoft Office アプリケーションのドキュメントに XML データを埋め込む方法について説明します。 ドキュメントに XML データを埋め込む場合、そのデータには「カスタム XML 部分」という名前が付きます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom XML parts [Office development in Visual Studio], about
- Office Open XML Formats [Office development in Visual Studio]
- custom XML parts [Office development in Visual Studio]
- embedding XML data in documents [Office development in Visual Studio]
- XML parts [Office development in Visual Studio]
- XML file formats [Office development in Visual Studio]
- data [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- XML [Office development in Visual Studio], custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- documents [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f6018f7e440eb0cc3cc0b7dcb113583aaf7fcd4e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99850010"
---
# <a name="custom-xml-parts-overview"></a>カスタム XML 部分の概要
  一部の Microsoft Office アプリケーションのドキュメントに XML データを埋め込むことができます。 XML データをドキュメントに埋め込むと、そのデータには *カスタム XML 部分* の名前が付けられます。

 Visual Studio で VSTO アドインまたはドキュメント レベルのソリューションを使用して、ドキュメントのカスタム XML 部分を作成または変更できます。 カスタム XML 部分を作成または変更するために Microsoft Office アプリケーションを開始する必要はありません。

 **適用対象:** このトピックの情報は、Excel、PowerPoint、および Word のドキュメントレベルのプロジェクトおよび VSTO アドインのプロジェクトに適用されます。 詳細については、「 [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

> [!NOTE]
> Visual Studio では、ドキュメント レベルのカスタマイズ内のデータ オブジェクトをキャッシュすることもできます。 いくつかの類似点はありますが、この機能はカスタム XML 部分とは異なります。 詳細については、「 [ドキュメントレベルのカスタマイズでのキャッシュ](../vsto/cached-data-in-document-level-customizations.md)されたデータ」を参照してください。

## <a name="understand-custom-xml-parts"></a>カスタム XML 部分について
 カスタム XML 部分は、2007 Microsoft Office system で Open XML 形式とともに導入されました。 これらの形式には、Excel、PowerPoint、および Word 用の XML ベースの新しいファイル形式 ( *.xlsx*、 *.pptx*、 *.docx* など) が含まれています。 これらの形式のドキュメントは、ZIP アーカイブ内のフォルダーに整理された XML ファイル (名前付き *xml 部分*) で構成されます。 XML 部分のほとんどは、ドキュメントの構造と状態を定義するのに役立つ組み込みの部分です。 ただし、ドキュメントにはカスタム XML 部分を含めることができ、ユーザーはこれを使用して、ドキュメントに任意の XML データを格納できます。

 XML ファイル形式を使用すると、古いバイナリファイル形式 ( *.xls*、 *.ppt*、 *.doc* など) ではできない方法で、アプリケーションがドキュメントを操作できるようになります。 ZIP アーカイブを読み取ることができるすべてのアプリケーションは、Microsoft Office がインストールされていない場合でも、ドキュメントの内容を検証し、変更できます。

 Open XML およびカスタム XML 部分の構造の詳細については、次の記事をご覧ください。

- [Office (2007) Open XML ファイル形式の概要](/previous-versions/office/developer/office-2007/aa338205(v=office.12))

- [方法: Open XML formats ドキュメントを操作する](/previous-versions/office/developer/office-2007/aa982683(v=office.12))

- [チュートリアル: Word 2007 XML 形式](/previous-versions/office/developer/office-2007/bb266220(v=office.12))

- [Open XML 形式を使用して Word 2007 ドキュメントを作成する](/previous-versions/office/developer/office-2007/bb264572(v=office.12))

> [!NOTE]
> Excel、Word、および PowerPoint ではバイナリ ファイル形式で保存されているドキュメント内のカスタム XML 部分を使用することもできます。 ただし、バイナリ形式でドキュメントを保存する場合は、Microsoft Office アプリケーションを起動せずにカスタム XML 部分を追加または変更することはできません。

## <a name="create-and-modify-custom-xml-parts"></a>カスタム XML 部分の作成および変更
 ドキュメントが Office アプリケーションで開いているとき、またはドキュメントが閉じているとき (Microsoft Office がインストールされていない場合でも)、カスタム XML 部分を作成または変更できます。

### <a name="modify-xml-parts-while-the-office-application-is-running"></a>Office アプリケーションの実行中に XML 部分を変更する
 ドキュメントレベルのカスタマイズまたは VSTO アドインを使用して、カスタム XML 部分を操作できます。 ドキュメント レベルのカスタマイズを使用している場合は、通常、カスタマイズされたドキュメント内にあるカスタム XML 部分を操作します。 VSTO アドインを使用している場合は、アプリケーションで開いている任意のドキュメントでカスタム XML 部分を作成または変更できます。

 Visual Studio を使用してカスタム XML 部分を作成するには、新しい <xref:Microsoft.Office.Core.CustomXMLPart> をドキュメントの <xref:Microsoft.Office.Core.CustomXMLParts> コレクションに追加します。 詳細については、次のトピックを参照してください。

- [方法: ドキュメントレベルのカスタマイズにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)

- [方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)

### <a name="modify-xml-parts-without-starting-the-office-application"></a>Office アプリケーションを起動せずに XML 部分を変更する
 Excel、PowerPoint、または Word を起動しないでカスタム XML 部分を変更できます。 これは、Microsoft Office アプリケーションがインストールされていないサーバーなどのコンピューターで、ドキュメント内の XML データを使用する場合に便利です。

 Microsoft Office を起動せずにカスタム XML 部分を追加するには Open XML SDK のクラスを使用します。 これらのクラスは、Office ドキュメントに固有の Open XML コンテンツにアクセスするために設計されています。 たとえば、カスタム XML 部分を Excel ブックに追加するには、 <xref:DocumentFormat.OpenXml.Packaging.OpenXmlPartContainer.AddNewPart%2A> オブジェクトのメソッドを使用し <xref:DocumentFormat.OpenXml.Packaging.WorkbookPart> ます。 詳細については、「 [OPEN XML SDK](/office/open-xml/open-xml-sdk)」を参照してください。

## <a name="bind-custom-xml-parts-to-word-content-controls"></a>カスタム XML 部分を Word コンテンツコントロールにバインドする
 Word ソリューションのコンテンツ コントロールをカスタム XML 部分の要素にバインドできます。 カスタム XML 部分にコンテンツ コントロールがバインドされると、カスタム XML 部分のデータがコンテンツ コントロールのユーザー インターフェイス (UI) に表示されます。 ユーザーがコントロール内のテキストを編集すると、対応する XML 要素が自動的に更新されます。 同様に、カスタム XML 部分の要素の値が変更されると、その XML 要素にバインドされているコンテンツ コントロールに新しいデータが表示されます。 詳細については、「 [コンテンツコントロール](../vsto/content-controls.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメントレベルのカスタマイズにおける XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
- [方法: ドキュメントレベルのカスタマイズにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)
- [方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)
- [コンテンツコントロール](../vsto/content-controls.md)
- [チュートリアル: カスタム XML 部分へのコンテンツコントロールのバインド](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)
