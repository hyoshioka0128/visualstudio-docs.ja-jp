---
title: C++ によるクロスプラットフォーム モバイル開発をインストールする | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: aaea6b8d-55eb-4427-8185-c050f855c257
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: c3ea8c91c54586cf54b82566a4803b464e01750c
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916490"
---
# <a name="install-cross-platform-mobile-development-with-c"></a>C++ によるクロスプラットフォーム モバイル開発をインストールする

Visual Studio で C++ を使うと、Windows デスクトップ アプリ、ユニバーサル Windows プラットフォーム (UWP) アプリ、Linux アプリ、そして今では Android および iOS 用のアプリも、ビルドできます。 **C++ によるモバイル開発**ワークロードは、Visual Studio にインストール可能なコンポーネントのセットであり、クロスプラットフォームの iOS、Android、および UWP Visual Studio テンプレートを含みます。 すぐに始めるために必要なクロスプラットフォーム ツールおよび SDK がインストールされるので、それらを自分で検索、ダウンロード、構成する必要はありません。 これらのツールを Visual Studio で使用することで、クロスプラットフォーム プロジェクトを簡単に作成、編集、デバッグ、テストできます。 この記事では、Visual Studio を使って C++ でクロスプラットフォーム アプリを開発するために必要なツールとサード パーティのソフトウェアをインストールする方法について説明します。 概要については、「[Visual C++ クロスプラットフォーム モバイル](https://visualstudio.microsoft.com/vs/features/cplusplus-mdd/)」を参照してください。

## <a name="requirements"></a>必要条件

::: moniker range="vs-2017"

- インストール要件については、「[Visual Studio 2017 製品ファミリのシステム要件](/visualstudio/productinfo/vs2017-system-requirements-vs)」を参照してください。

   > [!IMPORTANT]
   > Windows 7 または Windows Server 2008 R2 を使用している場合は、Windows デスクトップ アプリケーション、Android Native Activity アプリおよびライブラリ、iOS 用のアプリとコード ライブラリのためのコードを開発できますが、Windows Store アプリまたは UWP アプリのコードは開発できません。

::: moniker-end
::: moniker range=">=vs-2019"

- インストール要件については、「[Visual Studio 2017 製品ファミリのシステム要件](/visualstudio/releases/2019/system-requirements)」を参照してください。

   > [!IMPORTANT]
   > Windows 7 または Windows Server 2008 R2 を使用している場合は、Windows デスクトップ アプリケーション、Android Native Activity アプリおよびライブラリ、iOS 用のアプリとコード ライブラリのためのコードを開発できますが、Windows Phone アプリまたは UWP アプリのコードは開発できません。

::: moniker-end

特定のデバイス プラットフォームのアプリをビルドするには、いくつかの追加要件があります。

- Android SDK に付属している x86 Android エミュレーターは、Intel Hardware Accelerated Execution Manager (HAXM) などのハードウェア アクセラレータを使用できるコンピューターで最適に動作します。 詳細については、「[エミュレーターのパフォーマンスのためのハードウェア高速化 (Hyper-V と HAXM)](/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin&pivots=windows)」を参照してください。

- iOS 用のコードをビルドするには、Apple ID、iOS Developer Program アカウント、[Xcode](https://developer.apple.com/xcode/) バージョン 10.2 以降を OS X Mavericks (バージョン 10.9) 以降のバージョンで実行できる Mac コンピューターが必要です。 インストール手順のリンクについては、「[iOS 用ツールのインストール](#install-tools-for-ios)」をご覧ください。

- Windows Phone エミュレーターには、Hyper-V を実行できるコンピューターが必要です。 エミュレーターをインストールして実行する前に、Windows の Hyper-V 機能を有効にする必要があります。 詳細については、エミュレーターの「 [システム要件](system-requirements-for-the-visual-studio-emulator-for-android.md)」を参照してください。

## <a name="get-the-tools"></a>ツールを取得する

C++ でのモバイル開発は、Visual Studio の Community、Professional、Enterprise エディションで利用できます。 Visual Studio を入手するには、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページにアクセスしてください。 クロスプラットフォーム モバイル開発ツールは、Visual Studio 2015 以降で利用できます。

## <a name="install-the-tools"></a>ツールのインストール

Visual Studio インストーラーには、**C++ によるモバイル開発**ワークロードが含まれます。 このワークロードでは、Visual Studio での Android および iOS の開発に必要な C++ 言語のツール、テンプレート、コンポーネントがインストールされます。 Android のビルドとデバッグに必要な GCC や Clang ツール セット、Android SDK、および iOS 開発用の Mac と通信するコンポーネントが含まれます。 また、iOS および Android アプリの開発をサポートするために必要な他のサードパーティ製のツールとソフトウェア開発キットもすべてインストールされます。 これらのサードパーティ製ツールのほとんどは、Android プラットフォームのサポートに必要なオープン ソースのソフトウェアです。

- Android Native Development Kit (NDK)、Apache Ant、および C++ Android 開発ツールは、Android プラットフォームを対象にした C++ コードをビルドする場合に必要になります。

- Google Android Emulator および Intel Hardware Accelerated Execution Manager (HAXM) は、オプションですがお勧めするコンポーネントです。 (Intel HAXM ドライバーは Intel プロセッサでのみ動作し、Hyper-V を含む一部の VM とは互換性がありません)。Android デバイス上で直接開発およびデバッグできますが、通常、デバッグにはデスクトップでエミュレーターを使う方が簡単です。

- iOS プラットフォームを対象とする C++ コードをビルドするには、C++ iOS 開発ツールが必要です。

> [!NOTE]
> Visual Studio 2015 を使用している場合は、「[Visual C++ for Cross-Platform Mobile Development のインストール (Visual Studio 2015)](install-visual-cpp-for-cross-platform-mobile-development.md?view=vs-2015)」をご覧ください

### <a name="install-the-mobile-development-with-c-workload"></a>C++ によるモバイル開発ワークロードをインストールする

1. **[スタート]** メニューから **Visual Studio インストーラー**を実行します。

1. Visual Studio が既にインストールされている場合は、インストールされている Visual Studio の中で変更するバージョンの **[変更]** ボタンをクリックします。 それ以外の場合は、 **[インストール]** を選んで Visual Studio をインストールします。

1. **[ワークロード]** タブで、下にスクロールして、Visual Studio インストーラーの **[C++ によるモバイル開発]** ワークロードを選びます。 このワークロードを選ぶと、C++ による開発に必要な他のコンポーネントも選択されます。 他のワークロードを選び、個々のコンポーネントを同時にインストールすることもできます。 UWP もターゲットとするクロスプラットフォームのコードをビルドするには、 **[ユニバーサル Windows プラットフォーム開発]** ワークロードを選びます。

1. **[インストールの詳細]** ウィンドウで、 **[C++ によるモバイル開発]** を展開します。 **[オプション]** セクションでは、NDK の追加バージョン、Google Android Emulator、Intel Hardware Accelerated Execution Manager、IncrediBuild ビルド アクセラレーション ツールを選ぶことができます。

1. 既定では、1 つまたは複数の Android SDK セットアップ コンポーネントが、ワークロードによって組み込まれます。 Android SDK の追加バージョンを使用できます。 インストールに追加するには、 **[個別のコンポーネント]** タブを選び、 **[SDK、ライブラリ、およびフレームワーク]** セクションまで下にスクロールして選びます。

1. **[変更]** または **[インストール]** ボタンを選んで、**C++ によるモバイル開発**ワークロードと他の選択したワークロードおよびオプションのコンポーネントをインストールします。

   インストールが完了したら、インストーラーを閉じて、コンピューターを再起動します。 サード パーティ製コンポーネントの一部の設定操作は、コンピューターを再起動するまで有効になりません。

   > [!IMPORTANT]
   > 確実にすべてを正しくインストールするには、再起動する必要があります。

1. Visual Studio を開きます。

## <a name="install-tools-for-ios"></a>Install tools for iOS

Visual Studio を使用して、iOS のコードを編集およびデバッグし、iOS シミュレーターまたは iOS デバイスに展開することができます。 ただし、ライセンスの制限により、コードのビルドはリモート環境の Mac で行う必要があります。 Visual Studio を使用して iOS アプリをビルドおよび実行するには、Mac 上にリモート エージェントをセットアップして構成する必要があります。 インストール方法、前提条件、構成オプションの詳細については、「[iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。 iOS 用にビルドするのでない場合は、この手順を省略できます。

## <a name="install-or-update-dependencies-manually"></a>手動による依存関係のインストールまたは更新

**C++ によるモバイル開発**ワークロード (または、Visual Studio 2015 では Visual C++ モバイル開発オプション) をインストールするときに、サードパーティの 1 つ以上の依存関係を Visual Studio インストーラーでインストールしないことにした場合、それらの依存関係は、後で「[ツールのインストール](#install-the-tools)」の手順に従ってインストールできます。 最新のサードパーティ製コンポーネントをインストールするため、Visual Studio インストーラーは定期的に更新されます。 それを使って、更新された SDK と NDK をインストールできます。 また、Visual Studio とは別にインストールまたは更新することもできます。

Android SDK ディレクトリにある SDK Manager アプリをもう一度実行すると、SDK を更新したり、オプション ツールや追加の API レベルをインストールしたりできます。 **[管理者として実行]** を使用して SDK Manager アプリを実行しなければ、更新のインストールが失敗する可能性があります。 Android アプリのビルドで問題が発生した場合は、SDK Manager を確認して、インストール済み SDK の更新プログラムの有無を調べてください。

Android SDK に付属する一部の Android エミュレーターを使用するには、ハードウェア アクセラレータのセットアップが必要になる場合があります。 詳細については、「[エミュレーターのパフォーマンスのためのハードウェア高速化 (Hyper-V と HAXM)](/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin)」を参照してください。

ほとんどの場合、Visual Studio によって、インストールしたサードパーティ製ソフトウェアの構成が検出され、内部環境変数にインストール パスが保持されます。 これらのクロス プラットフォーム開発ツールの既定のパスは、Visual Studio IDE でオーバーライドできます。

#### <a name="to-set-the-paths-for-third-party-tools"></a>サード パーティのツールのパスを設定するには

1. Visual Studio のメニュー バーで、 **[ツール]**  >  **[オプション]** の順に選びます。

1. **[オプション]** ダイアログ ボックスで、 **[クロス プラットフォーム]**  >  **[C++]**  >  **[Android]** の順に選びます。

   ![Android ツールのパスのオプション](../cross-platform/media/cppmdd_options_android.PNG "CPPMDD_Options_Android")

1. ツールが使用するパスを変更するには、パスの横にあるチェック ボックスをオンにして、テキスト ボックスでフォルダー パスを編集します。 参照ボタン ( **...** ) を使用して **[場所を選択]** ダイアログを開き、フォルダーを選ぶこともできます。

1. **[OK]** を選んで、カスタム ツール フォルダーの場所を保存します。

## <a name="see-also"></a>関連項目

- [iOS を使用してビルドするためのツールのインストールおよび構成](install-and-configure-tools-to-build-using-ios.md)
- [Visual C++ クロスプラットフォーム モバイル](https://visualstudio.microsoft.com/vs/features/cplusplus-mdd/)
