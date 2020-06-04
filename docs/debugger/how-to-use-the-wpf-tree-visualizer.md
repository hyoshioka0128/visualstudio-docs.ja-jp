---
title: '方法: WPF ツリー ビジュアライザーを使用する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- WPF, debugging
- debugging, WPF
ms.assetid: 2a1bf1cd-90f9-4d06-9fb4-1bfc925afef3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbc705a20f8d878d85dc6aba14c64178c76041ac
ms.sourcegitcommit: 978df2feb5e64228d2e3dd430b299a5c234cda17
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72888402"
---
# <a name="how-to-use-the-wpf-tree-visualizer"></a>方法: WPF ツリー ビジュアライザーを使用する
WPF ツリー ビジュアライザーを使用すると、WPF オプションのビジュアル ツリーを調べたり、ツリーに含まれるオブジェクトの WPF 依存関係プロパティを表示したりすることができます。 ビジュアル ツリーの詳細については、「[WPF のツリー](/dotnet/framework/wpf/advanced/trees-in-wpf)」を参照してください。 依存関係プロパティの詳細については、「[依存関係プロパティの概要](/dotnet/framework/wpf/advanced/dependency-properties-overview)」を参照してください。

 WPF ツリー ビジュアライザーを開くと、左側に **[ビジュアル ツリー]** 、右側に **[ _<名前>_ **:** _<型>_ のプロパティ]** ペインという 2 つのペインが表示されます。 任意のオブジェクトを **[ビジュアル ツリー]** ペインで選択すると、 **[ _<名前>_ **:** _<型>_ のプロパティ]** ペインが自動的に更新され、そのオブジェクトのプロパティが表示されます。

 > [!NOTE]
 > [ライブ ビジュアル ツリーとライブ プロパティ エクスプローラー](../xaml-tools/inspect-xaml-properties-while-debugging.md)を使用して WPF オブジェクトのビジュアル ツリーを調べることもできます。 WPF ツリー ビジュアライザーはレガシ機能であり、アクティブな開発ではありません。

### <a name="to-open-the-wpf-tree-visualizer"></a>WPF ツリー ビジュアライザーを開くには

1. データヒント、 **[ウォッチ]** ウィンドウ、 **[自動変数]** ウィンドウ、または **[ローカル]** ウィンドウで、WPF オブジェクト名の横の、虫眼鏡アイコンの横にある矢印をクリックします。

     ビジュアライザーの一覧が表示されます。

2. **[WPF ツリー ビジュアライザー]** をクリックします。

### <a name="to-search-the-visual-tree"></a>ビジュアル ツリーを検索するには

- **[ビジュアル ツリー]** ウィンドウで、検索する文字列を **[検索]** ボックスに入力します。

  WPF ツリー ビジュアライザーで、入力した文字列と一致するビジュアル ツリー内の最初のオブジェクトが即時に検索されます。 より正確に一致する項目を検索するには、次の文字を入力します。

  - ビジュアル ツリー内の次の一致項目に移動するには、 **[次へ]** をクリックします。

  - 前の一致項目に戻るには、 **[前へ]** をクリックします。

  - 検索条件を消去するには、 **[クリア]** をクリックします。

### <a name="to-search-the-properties-list"></a>プロパティ リストを検索するには

- **[ _<名前>_ **:** _<型>_ のプロパティ]** ペインで、検索する文字列を **[フィルター]** ボックスに入力します。

  WPF ツリー ビジュアライザーで、入力した文字列と一致するプロパティが即時に検索され、入力した文字列と一致したこれらのプロパティのみが一覧に表示されます。 より正確に一致する項目を検索するには、次の文字を入力します。

  - 検索条件を消去するには、 **[クリア]** をクリックします。

### <a name="to-close-the-visualizer"></a>ビジュアライザーを閉じるには

- ダイアログ ボックスの右上隅にある **[閉じる]** をクリックします。

## <a name="see-also"></a>関連項目
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)
- [WPF のツリー](/dotnet/framework/wpf/advanced/trees-in-wpf)
- [依存関係プロパティの概要](/dotnet/framework/wpf/advanced/dependency-properties-overview)
