---
title: '方法 : アプリケーション アイコンを指定する (Visual Basic、C#) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- icons [Visual Studio], application
- application properties [Visual Studio], icons
- application icons [Visual Studio]
ms.assetid: ad8e14ed-adc2-45b6-a0be-818b16d5616f
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 136fd00bea736af0f0c589c28eae597ff8fd558e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670703"
---
# <a name="how-to-specify-an-application-icon-visual-basic-c"></a>方法 : アプリケーション アイコンを指定する (Visual Basic、C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクトの `Icon` プロパティは、ファイル エクスプローラーと Windows タスク バーに表示されるコンパイルされたアプリケーションのアイコン ファイル (.ico) を指定します。

 `Icon` プロパティには、**プロジェクト デザイナー**の **[アプリケーション]** ウィンドウからアクセスできます。このプロパティには、リソースまたはコンテンツ ファイルとしてプロジェクトに追加されているアイコンの一覧が含まれています。

> [!NOTE]
> アプリケーションのアイコン プロパティを設定した後、アプリケーション内の各 **Window** または **Form** の `Icon` プロパティを設定することもできます。 Windows Presentation Foundation (WPF) スタンドアロン アプリケーションのウィンドウ アイコンの詳細については、<xref:System.Windows.Window.Icon%2A> プロパティを参照してください。

### <a name="to-specify-an-application-icon"></a>アプリケーション アイコンを指定するには

1. **ソリューション エクスプローラー**で、 **[ソリューション]** ノードではなくプロジェクト ノードを選びます。

2. メニュー バーで、 **[プロジェクト]** 、 **[プロパティ]** の順に選びます。

3. **プロジェクト デザイナー**が表示されたら、 **[アプリケーション]** タブを選びます。

4. **(Visual Basic)** **[アイコン]** 一覧で、アイコン (.ico) ファイルを選びます。

     **(C#)** **[アイコン]** 一覧の近くにある **\<[参照]** ボタンを選び、使うアイコン ファイルの場所を参照します。

## <a name="see-also"></a>参照
 [[アプリケーション] ページ (プロジェクトデザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md) [[アプリケーション]C#ページ、プロジェクトデザイナー () アプリケーションの](../ide/reference/application-page-project-designer-csharp.md)[プロパティの管理](../ide/application-properties.md)[方法: リソースを追加または削除](https://msdn.microsoft.com/7b77bc06-3952-4799-b029-def3f8f7f88d)する
