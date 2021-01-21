---
title: XML リテラルと XML スキーマ エクスプローラーの統合
description: Visual Studio の XML スキーマ エクスプローラーで XML リテラルのサポートを使用して、XML フラグメントを Visual Basic コードに直接統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 57a29998-c6e8-48ac-bdb0-5788e73f9164
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 059263f06421fee3c90f2471df4c8b2c7bf8fc86
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93398502"
---
# <a name="integration-of-xml-literals-with-xml-schema-explorer"></a>XML リテラルと XML スキーマ エクスプローラーの統合

Visual Basic では XML リテラルがサポートされています。つまり、XML フラグメントを Visual Basic コードに直接組み込むことができます。 詳細については、「[XML リテラルの概要](/dotnet/visual-basic/programming-guide/language-features/xml/xml-literals-overview)」を参照してください。

## <a name="how-to"></a>方法

Visual Basic プロジェクトの XSD ファイルに XML リテラルが含まれる場合、**XML スキーマ エクスプローラー** で XML スキーマ セットを表示できます。 XML リテラルに関連付けられたスキーマ セットを表示するには、XML リテラルまたは XML 名前空間インポート内で XML ノードを右クリックして、 **[スキーマ エクスプローラーで表示]** コマンドをクリックします。

![[Show in Schema Explorer]\(スキーマ エクスプローラーで表示\) コマンドが強調表示された XML ノードのコンテキスト メニューを示す Visual Basic プロジェクト ウィンドウのスクリーンショット。](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer1.gif)

これにより、**XML スキーマ エクスプローラー** が Visual Basic ファイルと並んで表示されます。

![XML スキーマ エクスプローラーとソリューション エクスプローラーが右側のペインで開かれていることを示す Visual Basic プロジェクト ウィンドウのスクリーンショット。](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer2.gif)

## <a name="see-also"></a>関連項目

- [方法: XML リテラルに XML スキーマ デザイナーを使用する](../xml-tools/how-to-use-the-xml-schema-designer-with-xml-literals.md)
