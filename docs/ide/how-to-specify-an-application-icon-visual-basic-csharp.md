---
title: '方法: アプリケーション アイコンを指定する (Visual Basic、C#)'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- icons [Visual Studio], application
- application properties [Visual Studio], icons
- application icons [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 20e5d8a915c1621b26c070976f27db56d8f2c84e
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284062"
---
# <a name="how-to-specify-an-application-icon-visual-basic-c"></a>方法: アプリケーション アイコンを指定する (Visual Basic、C#)

プロジェクトの `Icon` プロパティでは、**ファイル エクスプローラー**と Windows タスク バーに表示されるコンパイルされたアプリケーションのアイコン ファイル ( *.ico*) を指定します。

`Icon` プロパティには、**プロジェクト デザイナー**の **[アプリケーション]** ウィンドウからアクセスできます。このプロパティには、リソースまたはコンテンツ ファイルとしてプロジェクトに追加されているアイコンの一覧が含まれています。

> [!NOTE]
> アプリケーションのアイコン プロパティを設定した後、アプリケーション内の各 **Window** または **Form** の `Icon` プロパティを設定することもできます。 Windows Presentation Foundation (WPF) スタンドアロン アプリケーションのウィンドウ アイコンの詳細については、<xref:System.Windows.Window.Icon%2A> プロパティを参照してください。

## <a name="to-specify-an-application-icon"></a>アプリケーション アイコンを指定するには

1. **ソリューション エクスプローラー**で、 **[ソリューション]** ノードではなくプロジェクト ノードを選びます。

1. メニュー バーで、 **[プロジェクト]**  >  **[プロパティ]** を選択します。

1. **プロジェクト デザイナー**が表示されたら、 **[アプリケーション]** タブを選びます。

1. **(Visual Basic)** &mdash; **[アイコン]** 一覧で、アイコン ( *.ico*) ファイルを選びます。

    **(C#)** &mdash; **[アイコン]** 一覧の近くにある **\<Browse...>** ボタンを選び、目的のアイコン ファイルの場所を参照します。

## <a name="see-also"></a>関連項目

- [[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)
- [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)
