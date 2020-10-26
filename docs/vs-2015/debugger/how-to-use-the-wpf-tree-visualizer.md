---
title: '方法: WPF ツリー ビジュアライザーを使用する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- WPF, debugging
- debugging, WPF
ms.assetid: 2a1bf1cd-90f9-4d06-9fb4-1bfc925afef3
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 381dc45351ae03e615afbdd31239869e3dba8e4e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825435"
---
# <a name="how-to-use-the-wpf-tree-visualizer"></a>方法: WPF ツリー ビジュアライザーを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

WPF ツリー ビジュアライザーを使用すると、WPF オプションのビジュアル ツリーを調べたり、ツリーに含まれるオブジェクトの WPF 依存関係プロパティを表示したりすることができます。 ビジュアル ツリーの詳細については、「[WPF のツリー](https://msdn.microsoft.com/library/e83f25e5-d66b-4fc7-92d2-50130c9a6649)」を参照してください。 依存関係プロパティの詳細については、「[依存関係プロパティの概要](https://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5)」を参照してください。  
  
 WPF ツリー ビジュアライザーを開くと、左側に **[ビジュアル ツリー]** 、右側に **[ _<名前>_ **:** _<型>_ のプロパティ]** ペインという 2 つのペインが表示されます。 任意のオブジェクトを **[ビジュアル ツリー]** ペインで選択すると、 **[ _<名前>_ **:** _<型>_ のプロパティ]** ペインが自動的に更新され、そのオブジェクトのプロパティが表示されます。  
  
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
  
- [**プロパティ**_名_**:**_型_] ペインで、検索する文字列を [**フィルター** ] ボックスに入力します。  
  
  WPF ツリー ビジュアライザーで、入力した文字列と一致するプロパティが即時に検索され、入力した文字列と一致したこれらのプロパティのみが一覧に表示されます。 より正確に一致する項目を検索するには、次の文字を入力します。  

  - 検索条件を消去するには、 **[クリア]** をクリックします。  
  
### <a name="to-close-the-visualizer"></a>ビジュアライザーを閉じるには  
  
- ダイアログ ボックスの右上隅にある **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [方法: ビジュアライザーを使用する](../misc/how-to-use-a-visualizer.md)   
 [カスタムビジュアライザーの作成](../debugger/create-custom-visualizers-of-data.md)   
 [WPF のツリー](https://msdn.microsoft.com/library/e83f25e5-d66b-4fc7-92d2-50130c9a6649)   
 [依存関係プロパティの概要](https://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5)
