---
title: セットアップとインストール | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 2cfcad00-352c-4161-814c-f5ae32d8ada8
caps.latest.revision: 19
ms.author: crdun
manager: crdun
ms.openlocfilehash: 430c54527ad0a4647bb750c505942242688aaa17
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297726"
---
# <a name="setup-and-install"></a>セットアップとインストール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Xamarin を使用して一般的な C#/.NET コード ベースからネイティブの iOS、Android、および Windows のアプリを作成するには、次の条件を満たす必要があります。  
  
- Windows アプリと Android アプリの開発: Visual Studio 2015 と Xamarin 4 がインストールされている Windows 開発用コンピューター (下記のメモを参照)。 ([Xamarin を直接インストールする](https://developer.xamarin.com/guides/cross-platform/getting_started/requirements/#install)手順 (xamarin.com) を実行すれば、Visual Studio 2013 を使うこともできます。)   
  
- iOS アプリの開発: XCode と Xamarin がインストールされている、OS X Yosemite (10.10.5) 以降を搭載した Mac。  
  
  Windows と Mac のコンピューターを同時にセットアップできます。また、インストーラーを実行している間に、「[Learn about mobile development with Xamarin (Xamarin によるモバイル開発の概要)](../cross-platform/learn-about-mobile-development-with-xamarin.md)」にアクセスして、必要な背景情報を読んだり見たりすることができます。  
 
このセットアップとインストールを実行した後、Xamarin を使用する上で問題がある場合は、[forums.xamarin.com](https://forums.xamarin.com/) に質問を投稿してください。
  
> [!NOTE]
> 2016 年 3 月 31 日の時点で、Visual Studio のすべてのエディションに付属のすべての Xamarin に追加のコストはかからず、別個のライセンスは必要ありません。 Xamarin Studio Community for Mac も、学生、OSS 開発者、小規模チームの場合には無料です。 以前の Xamarin ライセンスが構成されている Visual Studio の既存のインストールの場合は、Xamarin をバージョン 4.0.3.214 以降に更新する必要があることにご注意ください。 これを行うには、 **[ツール] > [オプション] > [Xamarin] > [その他]** の順に移動し、 **[今すぐ確認]** リンクをクリックして、4.0.3.214 更新プログラムをダウンロードします。 Visual Studio を再起動して、 **[ツール] > [Xamarin アカウント...]** に移動すると、更新の状況を確認できるはずです。  
  
 **このトピックの内容:**  
  
- [前提条件](#prereq)  
  
- [Windows のセットアップ (Visual Studio と Xamarin)](#windows)  
  
- [Mac のセットアップ (Apple ID、Xcode、および Xamarin)](#mac)  
  
## <a name="prereq"></a> 前提条件  
  
1. Windows と Android を対象とする場合:  
  
    1. 推奨: Windows 8 以降を実行しており、高速の Hyper-V ベースの Visual Studio Emulator for Android を使用できる (VM ではない) 物理 Windows コンピューター (Android デバイスを持っていない場合)。 (VM ではなく物理コンピューターが必要であることが書かれていましたか?)  
  
    1. Windows 7 以前のコンピューターを使用できます。その場合は、エミュレーターとして Xamarin Player for Android を使用します。 
    
    1. どちらの構成でも、接続された物理デバイス上では、いつでもアプリを直接実行できます。  
  
1. iOS を対象とする場合:  
  
    1. OS X 10.10.5 以降が動作する OS X Yosemite を搭載した、ネットワーク接続された Mac または Mac mini (Xcode 7.1 のために必要)。  
  
    1. 主要な開発環境として Windows (7 以降) コンピューターで Visual Studio を使う場合は、ネットワーク接続された Mac は、iOS アプリのコンパイルとデバッグ、iOS シミュレーターまたはテザリングされたデバイスへのアタッチ、または Visual Studio でユーザー インターフェイスを設計するためにストーリーボード デザイナーを使う場合にのみ必要になります。 この 2 次的な役割には、古いモデルの Mac で十分です。  
  
## <a name="windows"></a> Windows のセットアップ (Visual Studio と Xamarin)  
  
> [!TIP]
> 次の手順は、Visual Studio 2015 に適用されます。 Xamarin を Visual Studio 2013 (Update 2 が必要) で使うには、[Xamarin の直接インストール](https://developer.xamarin.com/guides/cross-platform/getting_started/requirements/#install) (xamarin.com) の指示に従ってください。  
  
1. [任意のエディションの Visual Studio 2015 のインストーラーをダウンロードして起動します](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) (Community、Professional、Enterprise)。 Visual Studio 2015 Community は、無料のエディションです。Professional および Enterprise の各エディションは評価版として 30 日間使用できます (その後はライセンスを購入する必要があります)。  
  
   1. 既に Visual Studio をインストールしてある場合は、 **[コントロール パネル] > [プログラムと機能]** を開き、 **[Visual Studio 2015]** の項目を選択して、 **[変更]** をクリックします。 インストーラーが表示されたら、 **[変更]** をクリックし、以下のステップ 3 にスキップします。  
  
2. (新規インストールの場合のみ) インストーラー内で **[カスタム]** インストールを選択します。  
  
    ![Visual Studio のインストールでの [カスタム] オプションの選択](../cross-platform/media/cross-plat-xamarin-setup-1.png "クロスプラットフォーム Xamarin セットアップ1")  
  
3. 次のチェック ボックスを選択します。  
  
   1. **[クロスプラットフォーム モバイル開発] > [C#/.NET (Xamarin)]** 。 これにより、[共通のツールとソフトウェア開発キット] の下のさまざまな Android ツールも自動的に選択されます。 このオプションでは、既存の Xamarin インストールも更新されるはずです。  
  
        ![[クロス&#45;プラットフォームモバイル開発] の [Xamarin] オプションを選択します。](../cross-platform/media/cross-plat-xamarin-setup-2.png "クロスプラットフォーム Xamarin セットアップ2")  
  
   2. Windows 8 以降の場合: **[クロスプラットフォーム モバイル開発] > [Microsoft Visual Studio Emulator for Android]** 。 注: Windows 7 またはそれ以前のコンピューターを使用している場合、または Mac 上で Windows を実行している場合は、これが*選択解除*されていることを確認してください。 ステップ 5 の後にある、「Windows コンピューター上のエミュレーターに関するメモ」をご覧ください。 この項目は、物理 Android デバイスでのみデバッグする予定の場合も、選択解除のままにしておくことができます。  
  
   3. (省略可能) Windows デバイスを対象とすることを計画している場合は、 **[Windows 開発と Web 開発] > [ユニバーサル Windows アプリ開発ツール]** または **[Windows 8.1 および Windows Phone 8.0/8.1 ツール]** も選択します (両方でもよい)。 これらには、ダウンロードに時間がかかるエミュレーター イメージをインストールするためのオプションが含まれています。いつでも Visual Studio インストーラーに戻って後で追加できます。  
  
4. [インストール] ボタンをクリックし、プロセスを実行します。 このプロセスでも、完了までにしばらく時間がかかります。その間、Mac のセットアップ手順を続行し、「[Xamarin を使用したモバイル開発について学習します](../cross-platform/learn-about-mobile-development-with-xamarin.md)」を読むことができます。  
  
5. インストールが完了したら、Visual Studio を起動し、アカウントを求められたら Microsoft アカウントでサインインします (これは Windows で使用するのと同じアカウントです)。 次に、 **[ツール] > [オプション] > [Xamarin]** または **[ツール] > [オプション] > [Xamarin] > [その他]** を選択して、Xamarin の更新プログラムを確認します。ここには **[今すぐ確認]** リンクが表示されます。  
  
    ![Visual Studio のオプションで Xamarin の更新プログラムを確認する](../cross-platform/media/cross-plat-xamarin-setup-3.png "クロスプラットフォーム Xamarin セットアップ3")  
  
   > [!NOTE]
   > 前述のとおり、以前の Xamarin でのライセンス問題を回避するために、Xamarin をバージョン 4.0.3.214 以上に更新してください。  

   **[ツール] > [オプション]** に Xamarin のオプションがない場合は、インストールをもう一度確認するか、Visual Studio を再起動してみてください。 または、[オプション] ダイアログで Xamarin を検索することもできます。
      
6. Windows 7 以前の場合、または Mac 上で Windows を実行している場合に、物理デバイスを持っていないときは、[Android SDK Emulator](https://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debug-on-emulator/android-sdk-emulator/) を使います。 下記のメモをご覧ください。  
  
   **Windows コンピューター上のエミュレーターに関するメモ:** CPU でサポートされる仮想化テクノロジは、一度に 1 つだけです。このため、開発用コンピューター上では 1 つのみを使用することをお勧めします。 主要な仮想化テクノロジには次の 3 つがあります。Hyper-V (Android 用の Visual Studio エミュレーターおよび Windows Phone エミュレーターで使用)、Virtual Box (Genymotion で使用)、Intel HAXM (Android SDK エミュレーターで使用)。 Hyper-V と Virtual Box 間にはさまざまな問題があるため、特定のコンピューター上では 1 種類のエミュレーターだけを使用することをお勧めします。したがって、Windows 8 以降のコンピューターでは Hyper-V を使用すること、および Windows 7 以前のコンピューターと Mac 上で実行している Windows では HAXM エミュレーターを使用することが前述のとおり推奨されます。  
  
## <a name="mac"></a> Mac のセットアップ (Apple ID、Xcode、および Xamarin)  
  
1. [https://appleid.apple.com](https://appleid.apple.com/) で無料の Apple ID を作成します (まだ作成していない場合)。 これは Xcode をインストールしてサインインするために必要です。  
  
2. [https://developer.apple.com/xcode/](https://developer.apple.com/xcode/) から Xcode をダウンロードしてインストールし、apple.com の「[Adding Your Account to XCode](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/AddingYourAccounttoXcode/AddingYourAccounttoXcode.html#//apple_ref/doc/uid/TP40013839-CH40-SW1)」 (XCode にアカウントを追加する) の説明に従って、Apple ID を追加します。  
  
3. 「 [Xamarin.iOS のダウンロードとインストール](https://docs.microsoft.com/xamarin/ios/get-started/installation/mac) 」(xamarin.com) の手順に従って、Xamarin をダウンロードしてインストールします。  
  
4. Windows と Mac のコンピューターの両方に Xamarin をインストールしたら、「[Connecting to the Mac (Mac への接続)](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/)」(xamarin.com) の手順に従って、Windows コンピューター上の Visual Studio から iOS と Mac を操作できるようにします。  
  
     両方のコンピューターが同じローカル ネットワーク上にある必要があることにご注意ください。
