---
title: 'チュートリアル: LinqToXmlDataBinding の例 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: aedf42e8-896c-48fa-88df-7f7c9536aa69
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0e97d612e19f64110f3090029dcff82acbad8e87
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663971"
---
# <a name="walkthrough-linqtoxmldatabinding-example"></a>チュートリアル : LinqToXmlDataBinding の例
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、LinqToXmlDataBinding の例を示し、L2DBForm.xaml と L2DBForm.xaml.cs という 2 つの主要なソース ファイルに関する興味深い情報をいくつか説明します。

## <a name="prerequisites"></a>必要条件
 このチュートリアルをお読みになる前に、「[方法 : LinqToXmlDataBinding という例をビルドして実行する](../designers/how-to-build-and-run-the-linqtoxmldatabinding-example.md)」の説明に従って、LinqToXmlDataBinding プログラムをビルドして実行することを強くお勧めします。

## <a name="remarks"></a>Remarks
 LinqToXmlDataBinding プログラムは、C# ソース ファイルと XAML ソース ファイルで構成される Windows Presentation Foundation (WPF) アプリケーションです。 このプログラムには書籍の一覧を定義する組み込み XML ドキュメントが含まれており、ユーザーはそれらのエントリを表示、追加、削除、および編集することができます。 このプログラムは、次の 2 つの主要なソース ファイルで構成されています。

- L2DBForm.xaml には、メイン ウィンドウのユーザー インターフェイス (UI) の XAML 宣言コードが含まれています。 また、書籍一覧のデータ プロバイダーと組み込み XML ドキュメントを定義するウィンドウ リソース セクションも含まれています。

- L2DBForm.xaml.cs には、UI に関連付けられている初期化メソッドとイベント処理メソッドが含まれています。

  メイン ウィンドウは縦に区切られ、次の 4 つの UI セクションに分かれています。

- **[XML]** には、組み込まれている書籍一覧の生の XML ソースが表示されます。

- **[Book List]** には書籍エントリが標準テキストで表示され、ユーザーはエントリを個別に選択および削除できます。

- **[Edit Selected Book]** では、ユーザーは現在選択している書籍エントリに関連付けられている値を編集できます。

- **[Add New Book]** では、ユーザーが入力した値に基づいて新しい書籍エントリを作成できます。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|-----------|-----------------|
|[L2DBForm.xaml ソース コード](../designers/l2dbform-xaml-source-code.md)|L2DBForm.xaml ファイルの XAML コードの内容と説明を示します。|
|[L2DBForm.xaml.cs Source Code](../designers/l2dbform-xaml-cs-source-code.md)|L2DBForm.xaml.cs ファイルの C# ソース コードの内容と説明を示します。|

## <a name="see-also"></a>参照
 [LINQ to XML 例を使用した WPF のデータバインディング](../designers/wpf-data-binding-using-linq-to-xml-example.md)[方法: LinqToXmlDataBinding の例をビルドして実行する](../designers/how-to-build-and-run-the-linqtoxmldatabinding-example.md)
