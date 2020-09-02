---
title: ツールウィンドウを使用した拡張機能の作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 94c8335b8d723ef20c04cfffe6b3788d71ecaa4f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431850"
---
# <a name="creating-an-extension-with-a-tool-window"></a>ツール ウィンドウでの拡張機能の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この手順では、VSIX プロジェクトテンプレートと **カスタムツールウィンドウ** 項目テンプレートを使用して、ツールウィンドウで拡張機能を作成する方法について説明します。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
### <a name="creating-a-tool-window"></a>ツールウィンドウの作成  
  
1. **Firstwindow**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. プロジェクトが開いたら、 **Firstwindow**という名前のツールウィンドウ項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[機能拡張** ] にアクセスし、[ **カスタムツールウィンドウ**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、ツールウィンドウのファイル名を **FirstWindow.cs**に変更します。  
  
3. プロジェクトをビルドし、デバッグを開始します。  
  
     Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。  
  
4. 実験用インスタンスで、[ **表示]/[その他のウィンドウ**] にアクセスします。  
  
     **Firstwindow**のメニュー項目が表示できます。 このボタンをクリックします。  
  
     「 **Firstwindow** 」というタイトルのツールウィンドウと、 **[click Me!** ] ボタンが表示されます。
