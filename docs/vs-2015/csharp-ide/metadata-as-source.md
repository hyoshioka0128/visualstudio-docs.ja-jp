---
title: ソースとしてのメタデータ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- Go To Definition command
- Code Definition window, viewing metadata as source
- metadata as source [C#]
ms.assetid: 4945a07f-b3be-4f05-a587-fc29058aa8fa
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b1d96224be13a12dcaadb394584f8441c7bd1934
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667523"
---
# <a name="metadata-as-source"></a>ソースとしてのメタデータ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソースとしてのメタデータにより、読み取り専用のバッファーで C# ソース コードとして表示されるメタデータを見ることができます。 これにより、型とメンバー (実装を含まない) の宣言のビューが使用できるようになります。 プロジェクトまたはソリューションから利用できないソースコードを持つ型またはメンバーに対して **[定義へ移動]** コマンドを実行すると、ソースとしてのメタデータを表示することができます。

> [!NOTE]
> 内部としてマークされている型またはメンバーに対して **[定義へ移動]** コマンドを実行しようとすると、統合開発環境 (IDE) には、参照元のアセンブリがフレンドかどうかに関係なく、ソースとしてのメタデータは表示されません。

 コード エディターまたは **[コード定義]** ウィンドウで、メタデータをソースとして表示できます。

## <a name="viewing-metadata-as-source-in-the-code-editor"></a>コード エディターでメタデータをソースとして表示
 ソースコードが使用不可能な項目に対して **[定義へ移動]** コマンドを実行すると、ソースとして表示されるその項目のメタデータのビューを含むタブ付きドキュメントがコード エディターで表示されます。 末尾に **[メタデータから]** が続く型の名前がドキュメントのタブに表示されます。

 たとえば、 **に対して** [定義へ移動] <xref:System.Console>コマンドを実行する場合は、その宣言に似ているものの、実装を持たない <xref:System.Console> のメタデータがコード エディターで C# ソース コードとして表示されます。

 ![ソースとしてのメタデータ](../csharp-ide/media/metadatasource.png "MetadataSource")

## <a name="viewing-metadata-as-source-in-the-code-definition-window"></a>[コード定義] ウィンドウでソースとしてメタデータを表示する
 **[コード定義]** ウィンドウがアクティブまたは表示されている場合、コード エディター内のカーソルの下の項目と **[クラス ビュー]** または **[オブジェクト ブラウザー]** で選ばれた項目に対して、IDE は **[定義へ移動]** コマンドを自動的に実行します。 その項目のソース コードが使用できない場合、IDE は項目のメタデータをソースとして **[コード定義]** ウィンドウに表示します。

 たとえば、コード エディターで <xref:System.Console> という単語内にカーソルを置く場合、 <xref:System.Console> のメタデータがソースとして **[コード定義]** ウィンドウに表示されます。 ソースは <xref:System.Console> 宣言に似ていますが、実装を持ちません。

 **[コード定義]** ウィンドウで表示される項目の宣言を確認するには、その項目を右クリックし、 **[定義へ移動]** をクリックします。