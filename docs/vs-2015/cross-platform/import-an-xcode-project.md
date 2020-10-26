---
title: XCode プロジェクトのインポート | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: aa4b8161-d98f-4a1a-9db3-520133bfc82f
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 4faa2ecae7f53d29e6aad92723ca6d12e50e2812
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150972"
---
# <a name="import-an-xcode-project"></a>XCode プロジェクトのインポート
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft Visual C++ for Cross-Platform Mobile Development には、XCode プロジェクトを Visual Studio に移動して、クロスプラットフォーム ライブラリを作成し、他のプロジェクトとコードを共有するためのサポートが含まれています。 [XCode からインポート] ウィザードを使うと、プロジェクトをインポートするプロセスと、C++ コードを分割して XCode ターゲットに取り込み、スタティック ライブラリまたは共有コード プロジェクトとして利用するプロセスが簡略化されます。 iOS 固有のコードを Visual Studio で管理しながらも、XCode を使ってストーリーボードとビルドを行うことができます。 Visual Studio と XCode の間でコードを双方向に簡単に移動する方法については、「Move Changes Between XCode and Visual Studio (XCode と Visual Studio 間の変更の移動)」を参照してください。  
  
## <a name="using-the-import-from-xcode-wizard"></a>[XCode からインポート] ウィザードの使用方法  
 このトピックでは、XCode プロジェクトを Visual Studio に移動して、コードの共有とクロスプラットフォーム ソリューションを活用する方法について説明します。 前提条件として、プロジェクトをインポート、エクスポート、ビルドできるように Mac を Visual Studio にペアリングする必要があります。 ペアリングを設定する手順については、「[iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。 また、[XCode からインポート] ウィザードで使うために、XCode プロジェクトをネットワーク経由で共有するか、Visual Studio コンピューターに移動する必要があります。  
  
#### <a name="import-from-xcode"></a>XCode からのインポート  
  
1. **[ファイル]** メニューで、**[新規作成]**、**[インポート]**、**[XCode からインポートする]** の順に選択します。 これにより、**[XCode からインポート]** ウィザードが開始されてダイアログが表示されます。  
  
    ![インポートする XCode ターゲットプロジェクトを選択します](../cross-platform/media/cppmdd-u2-importxcode-choose.PNG "CPPMDD_U2_ImportXCode_Choose")  
  
2. **[プロジェクトを選択]** ウィンドウで、[参照] ボタンを選択して XCode の .pbxproj ファイルを選びます。 **[XCode プロジェクト ファイルの選択]** ダイアログでプロジェクト ファイルに移動し、**[開く]** を選択します。  
  
    ![[XCode プロジェクト ファイルの選択] ダイアログでプロジェクト ファイルを選択する](../cross-platform/media/cppmdd-u2-importxcode-browse.PNG "CPPMDD_U2_ImportXCode_Browse")  
  
    [XCode からインポート] ウィザードで、**[次へ]** を選択します。  
  
3. **[宛先ターゲット]** ウィンドウで、Visual Studio プロジェクトにインポートする XCode プロジェクトからターゲットを選択します。 XCode ターゲットは、Visual Studio のプロジェクトに似ています。ほとんどのターゲットは、バイナリを生成するコードとリソースのコレクションです。 [XCode からインポート] ウィザードで宛先ターゲットとしてインポートできるのは、スタティック ライブラリではなく、バイナリを生成するターゲットだけです。 XCode スタティック ライブラリのターゲットは、次のステップで操作します。  
  
    ![XCode ウィザードの [ターゲットターゲット] ウィンドウからのインポート](../cross-platform/media/cppmdd-u2-importxcode-destination.jpg "CPPMDD_U2_ImportXCode_Destination")  
  
    **[インポートするターゲット]** で選択されている各ターゲットについて、ウィザードは、別個のスタティック ライブラリ プロジェクトに分割できる C++ コード ファイルを自動的に検出し、**[C++ プロジェクト項目]** セクションに置きます。 その他のコードおよびリソースは、**[XCode プロジェクト項目]** セクションに残ります。 これらの項目は、ウィザードによるインポート処理が完了すると、Visual Studio 内の別個のスタティック ライブラリおよびアプリケーション プロジェクトになります。 既定では、単体テストおよびフレームワークのターゲットは、ウィザードによって別個のプロジェクトには分割されません。  
  
    各プロジェクトに含めるファイルを変更するには、上矢印と下矢印のボタンを使います。 各プロジェクト内のファイルを適切に設定できたら、**[次へ]** を選択して、先へ進みます。  
  
4. **[ライブラリ ターゲット]** ウィンドウで、XCode プロジェクトから Visual Studio プロジェクトにインポートするスタティック ライブラリ ターゲットを選択します。 このウィンドウでは、共有コード プロジェクトに配置するファイルと、スタティック ライブラリ プロジェクトに配置するファイルを選択することができます。 **[インポートするターゲット]** リストに含まれる各ターゲットについて、**[共有コード プロジェクト項目]** と **[スタティック ライブラリ プロジェクト項目]** に配置するファイルを、上矢印と下矢印のボタンを使って制御できます。  
  
    ![XCode ライブラリターゲットウィンドウからのインポート](../cross-platform/media/cppmdd-u2-importxcode-library.jpg "CPPMDD_U2_ImportXCode_Library")  
  
    共有コード プロジェクトは、Visual Studio のプロジェクトとの間でソース コード ファイルのセットを共有する 1 つの方法です。 コードは、それ専用のプロジェクトとしてではなく、コードが含まれているプロジェクトの一部としてビルドされます。 共有コードを含むプロジェクトはさまざまなアーキテクチャと構成を対象にしている場合があるため、これは、さまざまな種類のプラットフォーム向けにビルドするコードが含まれた 1 つのプロジェクトを提供するための最適な方法です。  
  
    各プロジェクト内のファイルを適切に設定できたら、**[次へ]** を選択して、先へ進みます。  
  
5. **[グローバル プロパティ]** ウィンドウは、Visual Studio 内のすべての iOS プロジェクトに対してフレームワークの検索パスとインクルード ヘッダーの検索パスを設定するために使用できます。 Visual Studio では、ソース コードの参照と IntelliSense のためにこれらのパスを使います。 これらのグローバル パスは、ヘッダーとフレームワークの共通のセットを使う iOS プロジェクトを作成するときに役立ちます。  
  
    ![XCode グローバルプロパティペインからのインポート](../cross-platform/media/cppmdd-u2-importxcode-global.jpg "CPPMDD_U2_ImportXCode_Global")  
  
    これらのグローバルのパスは、Visual Studio の **[オプション]** ダイアログで設定することもできます。 それには、**[ツール]** メニューで、**[オプション]** を選択します。 **[オプション]** ダイアログで、**[クロス プラットフォーム]**、**[C++]**、**[iOS]**、**[グローバル プロパティ]** の順に展開します。  
  
    **[次へ]** を選択して続行します。  
  
6. **[フレームワーク]** ウィンドウでは、プロジェクトに対して参照と IntelliSense のために Visual Studio で使用されるパスを構成します。 これらのパスは、XCode プロジェクトによって参照される各フレームワークに対して、Visual Studio からアクセスできる必要があります。 ウィザードは、XCode プロジェクトのフレームワーク参照を確認し、Visual Studio からフレームワークを検索できるかどうかを表示します。 既にグローバル プロパティに設定してあるすべてのパスは、Visual Studio から検出できる必要があります。 例外は、フレームワーク リストに表示されます。 リストで X が付いているフレームワークごとに、Visual Studio がフレームワークを検索できるように、PC からアクセス可能なパスを指定してください。 参照ボタン [...] を使用すると、[ **フォルダーの選択** ] ダイアログボックスを使用してパスを検索できます。 フレームワークのパスは、ローカルのコピー、ネットワークでアクセスできる Mac 上の共有のいずれかを指定できます。  
  
    ![XCode Framework ペインからのインポート](../cross-platform/media/cppmdd-u2-importxcode-frameworks.jpg "CPPMDD_U2_ImportXCode_Frameworks")  
  
    **[次へ]** を選択して続行します。  
  
7. **[プロジェクト設定]** ウィンドウでは、ウィザードで作成した各プロジェクトのフレームワークとインクルード ヘッダー ファイルの検索パス設定を変更できます。 このウィンドウを使うと、グローバル設定とは異なるプロジェクト固有のパスを設定できます。  
  
    特定のプロジェクトのパスを設定するには、**[宛先のプロジェクト]** ドロップダウンでプロジェクト ファイルを選択した後、**[フレームワークの検索パス]** および **[インクルードヘッダーの検索パス]** コントロールに値を設定します。 各コントロールの横にある参照ボタン [...] を使うと、**[フォルダーの選択]** ダイアログを使ってパスを検索できます。  
  
    ![XCode プロジェクトウィンドウからのインポート](../cross-platform/media/cppmdd-u2-importxcode-projects.jpg "CPPMDD_U2_ImportXCode_Projects")  
  
    この PC とペアリングされているリモート Mac がない場合は、[リモート コンピューターを構成] リンクが表示されます。 ペアリングを設定する手順については、「[iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。  
  
    ウィザードの設定を使用して XCode プロジェクトをインポートするには、**[インポート]** を選択します。  
  
   [XCode からインポート] ウィザードによって、選択した XCode プロジェクト ターゲットに対応するプロジェクトが Visual Studio で作成されます。 他の C++ プロジェクトと共有できるコードは、別個の共有コード プロジェクトとスタティック ライブラリ プロジェクトに分割されます。 残りのコードは、iOS ライブラリ プロジェクトとアプリケーション プロジェクトに配置され、Visual Studio からリモートでビルドできます。 Visual Studio と XCode の間でコードを移動する方法の詳細については、「[XCode と Visual Studio 間の変更の同期](../cross-platform/sync-changes-between-xcode-and-visual-studio.md)」をご覧ください。
