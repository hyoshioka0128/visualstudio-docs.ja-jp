---
title: Xml リテラルと XML スキーマエクスプローラーの統合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 57a29998-c6e8-48ac-bdb0-5788e73f9164
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a15767454c83604de2844e4c0a9f2e121a9a1a4f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75846122"
---
# <a name="integration-of-xml-literals-with-xml-schema-explorer"></a>XML リテラルと XML スキーマ エクスプローラーの統合
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Basic では XML リテラルがサポートされています。つまり、XML フラグメントを Visual Basic コードに直接組み込むことができます。 詳細については、「 [XML リテラルの概要](https://msdn.microsoft.com/library/bb384629.aspx)」を参照してください。

 Visual Basic プロジェクトの XSD ファイルに XML リテラルが含まれる場合、XML スキーマ エクスプローラーで XML スキーマ セットを表示できます。 XML リテラルに関連付けられたスキーマ セットを表示するには、XML リテラルまたは XML 名前空間インポート内で XML ノードを右クリックして、 **[スキーマ エクスプローラーで表示]** コマンドをクリックします。

 ![Visual Basic XML リテラル (XML スキーマ エクスプローラー)](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer1.gif "VBXMLLiteralsWithXMLSchemaExplorer1")

 これにより、XML スキーマ エクスプローラーが Visual Basic ファイルと並んで表示されます。

 ![Visual Basic XML リテラル (XML スキーマ エクスプローラー)](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer2.gif "VBXMLLiteralsWithXMLSchemaExplorer2")

 この機能は Visual Studio 2008 SP1 で導入されました。 この機能の詳細については、「 [Channel 9 インタビュー: Visual Studio 2008 SP1 の XML スキーマエクスプローラー](https://channel9.msdn.com/Blogs/funkyonex/XML-Schema-Explorer-in-Visual-Studio-2008-SP1)」を参照してください。

## <a name="see-also"></a>参照
 [方法: xml リテラルで XML スキーマデザイナーを使用する](../xml-tools/how-to-use-the-xml-schema-designer-with-xml-literals.md)
