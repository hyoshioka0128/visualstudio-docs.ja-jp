---
title: '方法: ビジュアライザーを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
f1_keywords:
- vs.debug.dataviewer
- vs.debug.stringviewer
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, visualizers
- visualizers, about visualizers
ms.assetid: d2611385-0134-4387-8c5a-979fe625a462
caps.latest.revision: 37
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0f981b76d471658fe82e874901ad784a17841891
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "64778378"
---
# <a name="how-to-use-a-visualizer"></a>方法 : ビジュアライザーを使用する
ビジュアライザーを使用して、変数またはオブジェクトの内容を、データ型にとって意味のある方法で表示できます。 ビジュアライザーは、 **DataTips**、[ **ウォッチ** ] ウィンドウ、[ **自動変数** ] ウィンドウ、または [ **ローカル** ] ウィンドウから使用できます。  
  
 ビジュアライザーは、.NET Compact Framework ではサポートされていません。  
  
> [!NOTE]
> **ストア**アプリでは、標準のテキスト、HTML、XML、および JSON ビジュアライザーのみがサポートされています。 カスタム (ユーザーが作成した) ビジュアライザーはサポートされていません。  
  
### <a name="to-open-a-visualizer"></a>ビジュアライザーを開くには  
  
1. [ **DataTips**]、[ **ウォッチ** ] ウィンドウ、または [ **自動**変数]、[ **ローカル**]、または [ **クイックウォッチ** ] の各ウィンドウで、変数名の横に表示される虫眼鏡アイコンをクリックします。  
  
     ビジュアライザーの一覧が表示されます。  
  
2. 使用するビジュアライザーをクリックします。  
  
### <a name="to-use-a-visualizer-for-managed-code-during-remote-debugging"></a>リモート デバッグ中にマネージド コードにビジュアライザーを使用するには  
  
- デバッグ セッションを開始する前に、ビジュアライザー DLL をリモート コンピューターにコピーします。  
  
     DLL のパスは、リモート コンピューターとローカル コンピューター上で同じにする必要があります。 このパスは、次のいずれかの場所になります。  
  
     *Visual Studio のインストール パス* `\Common7\Packages\Debugger\Visualizers`  
  
     - または -  
  
     `My Documents\Visual Studio 2010\Visualizers`*Visual Studio のバージョン*`\Visualizers`  
  
## <a name="see-also"></a>参照  
 [カスタムビジュアライザーの作成](../debugger/create-custom-visualizers-of-data.md)   
 [方法: ビジュアライザーをインストールする](../debugger/how-to-install-a-visualizer.md)   
 [方法: ビジュアライザーを記述する](../debugger/how-to-write-a-visualizer.md)   
 [データ ヒントでのデータ値の表示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)