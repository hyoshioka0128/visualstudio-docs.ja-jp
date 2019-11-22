---
title: Visual Studio Tools for Unity の使用を開始する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
caps.latest.revision: 12
author: conceptdev
ms.author: crdun
manager: jillfra
ms.openlocfilehash: f110b8d6f7ab05d5a1b6942cd9ec599a8d8619b7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299821"
---
# <a name="getting-started-with-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity の使用を開始する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、Visual Studio Tools for Unity をインストールする方法と、Visual Studio で操作できるように Unity プロジェクトを構成する方法を説明します。  
  
> [!IMPORTANT]
> Unity 5.2 では Visual Studio Tools for Unity 2.1 の組み込みサポートが追加され、プロジェクトのセットアップが簡単になりました。 これを活用するには、Windows で Unity バージョン 5.2.0 以降と、Visual Studio Tools for Unity バージョン 2.1 以降が必要です。  
  
## <a name="prerequisites"></a>必要条件  
 Visual Studio Tools for Unity を使用するには、次のコンポーネントが必要です。  
  
- 拡張機能をサポートしているバージョンの **Visual Studio** (Visual Studio Community、Professional、Premium、Enterprise など)。 Visual Studio Community は無料でダウンロードできます。  
  
     [Visual Studio Community をダウンロード](https://www.visualstudio.com/downloads/download-visual-studio-vs)  
  
- **Unity** バージョン 4.0.0 以降、 **Unity** バージョン 5.2.0 以降 (Visual Studio Tools for Unity バージョン 2.1 以降の組み込みサポートを利用する場合)  
  
     [Unity をダウンロード](https://unity3d.com/get-unity/download)  
  
## <a name="install-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity のインストール  
 Visual Studio Tools for Unity を Visual Studio ギャラリーからダウンロードしてインストールします。 ご使用の Visual Studio バージョンに適したパッケージをインストールする必要があります。 Unity 5.2 以降で VSTU の組み込みサポートを利用するには、Visual Studio Tools for Unity バージョン 2.1 以降をインストールしてください。  
  
- Visual Studio 2015 Community、Visual Studio 2015 Professional、または Visual Studio 2015 Enterprise の場合:  
  
     [Visual Studio 2015 Tools for Unity をダウンロード](https://visualstudiogallery.msdn.microsoft.com/8d26236e-4a64-4d64-8486-7df95156aba9)  
  
- Visual Studio 2013 Community、Visual Studio 2013 Professional、または Visual Studio 2013 Premium の場合:  
  
     [Visual Studio 2013 Tools for Unity をダウンロード](https://visualstudiogallery.msdn.microsoft.com/20b80b8c-659b-45ef-96c1-437828fe7cf2)  
  
- Visual Studio 2012 Professional または Visual Studio 2012 Premium の場合:  
  
     [Visual Studio 2012 Tools for Unity をダウンロード](https://visualstudiogallery.msdn.microsoft.com/7ab11d2a-f413-4ed6-b3de-ff1d05157714)  
  
- Visual Studio 2010 Professional または Visual Studio 2010 Premium の場合:  
  
     [Visual Studio 2010 Tools for Unity をダウンロード](https://visualstudiogallery.msdn.microsoft.com/6e536faa-ce73-494a-a746-6a14753015f1)  
  
> [!NOTE]
> Visual Studio Express バージョンは、Visual Studio Tools for Unity などの拡張機能をサポートしていません。 Visual Studio Community は、Visual Studio Tools for Unity と他の拡張機能をサポートしている無料版の Visual Studio です。 ほとんどのユーザーの場合、Visual Studio Community が Express よりも適した選択肢になります。  
  
## <a name="your-first-unity-project-with-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity で取り組む最初の Unity プロジェクト  
 これで必要なすべてが揃ったので、Visual Studio による初めての Unity プロジェクトに取り組む準備が整いました。 Unity プロジェクトの設定は、インストールされている Unity と Visual Studio Tools for Unity のバージョンによって異なります。 次の手順で、インストールされている Unity と Visual Studio Tools for Unity のバージョンを確認します。  
  
### <a name="unity-52-and-higher-requires-vstu-21-or-higher"></a>Unity 5.2 以降 (VSTU 2.1 以降が必要)  
 Unity 5.2 以降では、Visual Studio Tools unitypackage をプロジェクトにインポートする必要がなくなりました。 プロジェクトによりこの unitypackage がインポートされると、Unity 5.2 はこれを無視し、Visual Studio Tools for Unity をインストール場所から直接読み込みます。  
  
#### <a name="1---create-a-unity-project"></a>1 - Unity プロジェクトの作成  
 これまでに Unity を使用した経験がある場合は、新しいプロジェクトを作成するか、または独自のプロジェクトを読み込むことができます。 古いバージョンの Unity で Visual Studio Tools for Unity を使用するために、Visual Studio Tools unitypackage をインポートしたプロジェクトを読み込む場合は、UnityVS ディレクトリを削除してそのパッケージを削除することをお勧めします。  
  
 それ以外の場合で Unity を初めて使用するときには、基本的なチュートリアルを使用して小規模なものから始めます。 Unity の学習ページを参照して、手始めに作業できるサンプル プロジェクトのチュートリアルや、Unity を使用した独自のゲームの作成方法を学ぶためのレッスンを見つけます。 Unity の学習ページには、異なるいくつかのゲームのわかりやすいチュートリアルがあります。  
  
 [チュートリアル – Unity の学習ページ](https://learn.unity.com/tutorials)  
  
#### <a name="2---configure-unity-editor-to-use-visual-studio-tools-for-unity"></a>2 - Visual Studio Tools for Unity を使用するための Unity エディターの構成  
 プロジェクトで Visual Studio Tools for Unity を使用できるようにするには、Visual Studio を外部スクリプト エディターとして設定するだけです。 Unity エディターのメイン メニューで **[Edit]、[Preferences]** を選び、次に **[Unity Preferences]** ダイアログで **[External Tools]** を選びます。 次に、使用する Visual Studio のバージョンを **[External Script Editor]** プロパティに設定し (この Visual Studio バージョンに対応した Visual Studio Tools for Unity がインストールされている必要があります)、 **[Editor Attaching]** プロパティが設定されていることを確認します。  
  
 Visual Studio Tools for Unity の組み込みサポートが有効であることを確認するため、 **[About Unity]** ダイアログを表示します。 In the Unity editor, on the main menu, choose **[Help]、[About Unity]** を選びます。Visual Studio Tools for Unity がインストールされており、正しく構成されている場合は、 **[About Unity]** ダイアログを表示します。  
  
 最後に、 **[Build Settings]** ページでビルド ターゲットが設定されていることと、 **[Script Debugging]** が有効になっていることをご確認ください。  
  
 ![Configure the Unity build settings for debugging.](../cross-platform/media/vstu-debugging-build-settings.png "vstu_debugging_build_settings")  
  
#### <a name="3---launch-visual-studio-from-the-unity-editor"></a>3 - Unity エディターからの Visual Studio の起動  
 Unity 5.2 以降では、Visual Studio を起動する場合や Visual Studio Tools for Unity を設定する場合に **[Visual Studio Tools]** 拡張機能メニューは不要になりました。 代わりに、Visual Studio が外部スクリプト エディターとして構成されたら、Unity エディターでそのスクリプト ファイルを選ぶだけで、コードが Visual Studio で開きます。  
  
### <a name="previous-versions-of-unity-pre-52"></a>以前のバージョンの Unity (5.2 以前)  
 Unity 5.2 より前のバージョンでは、Visual Studio Tools for Unity の組み込みサポートがありませんでした。 代わりに、Visual Studio Tools for Unity を使用するためには各プロジェクトで Visual Studio Tools unitypackage をインポートし、その他のプロジェクト設定を構成する必要がありました。  
  
#### <a name="1---create-a-unity-project"></a>1 - Unity プロジェクトの作成  
 これまでに Unity を使用した経験がある場合は、新しいプロジェクトを作成するか、または独自のプロジェクトを読み込むことができます。 新しいプロジェクトを開始する場合は、プロジェクトの作成時に Visual Studio Tools unitypackage をインポートします。  
  
 それ以外の場合で Unity を初めて使用するときには、基本的なチュートリアルを使用して小規模なものから始めます。 Unity の学習ページを参照して、手始めに作業できるサンプル プロジェクトのチュートリアルや、Unity を使用した独自のゲームの作成方法を学ぶためのレッスンを見つけます。 Unity の学習ページには、異なるいくつかのゲームのわかりやすいチュートリアルがあります。  
  
 [チュートリアル – Unity の学習ページ](https://learn.unity.com/tutorials)  
  
#### <a name="2---configure-unity-editor-to-use-visual-studio-tools-for-unity"></a>2 - Visual Studio Tools for Unity を使用するための Unity エディターの構成  
 既存の Unity プロジェクトを使って開始する場合、あるいはプロジェクトの作成時に Visual Studio Tools unitypackage をインポートしなかった場合は、この時点で unitypackage をインポートしなければなりません。 Unity エディターのメイン メニューで、 **[Assets]、[Import Package]、[Visual Studio 2015 Tools]** (インストールされているバージョンの Visual Studio 用オプションが表示されます) を選びます。  
  
 ![Import the VSTU package into your Unity project.](../cross-platform/media/vstu-configure-unity-import-vstu.png "vstu_configure_unity_import_vstu")  
  
 最後に、 **[Build Settings]** ページでビルド ターゲットが設定されていることと、 **[Script Debugging]** が有効になっていることをご確認ください。  
  
 ![Configure the Unity build settings for debugging.](../cross-platform/media/vstu-debugging-build-settings.png "vstu_debugging_build_settings")  
  
#### <a name="3---launch-visual-studio-from-unity-editor"></a>3 - Unity エディターからの Visual Studio の起動  
 最後の手順として Unity から Visual Studio を起動します。 これにより、プロジェクト用の Visual Studio ソリューションが作成され、Visual Studio で開かれます。  
  
 Unity エディターのメイン メニューで、 **[Visual Studio Tools]、[Open in Visual Studio]** を選びます。  
  
 ![Open your unity project in Visual Studio.](../cross-platform/media/vstu-configure-open-in-visual-studio.png "vstu_configure_open_in_visual_studio")  
  
## <a name="next-steps"></a>次のステップ  
 Visual Studio で Unity プロジェクトを操作およびデバッグする方法については、「 [Using Visual Studio Tools for Unity](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [Unity ホームページ](https://unity.com/)
