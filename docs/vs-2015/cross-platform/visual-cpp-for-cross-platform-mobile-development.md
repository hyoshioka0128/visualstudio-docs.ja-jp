---
title: Visual C++ for Cross Platform Mobile Development | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 0bb872d6-981b-4c96-9143-fcec5336bf0d
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: e947800c82036b061b2f48303733690a95ec53bc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62573067"
---
# <a name="visual-c-for-cross-platform-mobile-development"></a>Visual C++ for Cross-Platform Mobile Development
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ for Cross-Platform Mobile Development を使用することによって、iOS、Android、および Windows デバイス対応のネイティブ C++ アプリをビルドし、iOS、Android、および Windows 用に作成されたライブラリ内で共通コードを共有できます。 これは、Visual Studio 2015 で使用できるオプションです。このオプションを選択すると、共有ライブラリとネイティブ アプリのクロスプラットフォーム開発に必要な SDK とツールがインストールされます。 インストールされている場合、Windows、Windows Phone、および Xbox に加え、iOS と Android のデバイスおよびプラットフォームで実行されるコードを、Visual C++ を使用して作成できます。  
  
 複数のプラットフォーム用にコードを記述することは、ストレスのたまる作業になることがあります。 iOS、Android、および Windows の主要な開発言語とツールは、それぞれのプラットフォームによって異なります。 ただし、すべてのプラットフォームは共通して C++ コードの記述をサポートしています。 この共通項を利用して、プラットフォーム間でのコードの再利用を可能にすることができます。 C++ で記述されたネイティブ コードは、パフォーマンスに優れているだけでなく、リバース エンジニアリングに対する耐性もあります。 コードを再利用できれば、複数のプラットフォーム用にアプリを作成する場合にかかる時間と労力の両方を節約できます。  
  
 Visual C++ for Cross-Platform Mobile Development を使用した開発には、次の利点があります。  
  
1. **インストールが簡単。** Visual Studio インストーラーによって、Android と iOS のアプリまたはライブラリを作成するために必要となるサード パーティ製のツールと SDK が取得され、インストールされます。 構成とセットアップは単純で、ほとんどが自動的に行われます。  
  
2. **強力で使い慣れたビルド環境。** Visual Studio テンプレートを使用して、共有可能なクロスプラットフォーム ソリューションおよびプロジェクトを簡単に作成できます。 1 つの共通インターフェイスを使用して、すべてのプロジェクトのプロパティを管理できます。 すべてのコードを Visual Studio エディターで編集できるため、組み込みのクロスプラットフォーム IntelliSense のコード補完機能とエラーの強調表示を利用できます。  
  
3. **統合されたデバッグ操作。** Android デバイスおよびエミュレーター、iOS シミュレーターおよびデバイス、Windows または Windows Phone デバイスおよびエミュレーターを含めたすべてのプラットフォームで、Visual Studio の国際的レベルのデバッグ ツールを使用して、C++ コードを観察しながらステップ実行できます。  
  
## <a name="get-the-tools"></a>ツールの入手  
 Visual C++ for Cross-Platform Mobile Development は、Visual Studio 2015 に付属しているインストール可能なオプションです。 前提条件とインストール手順については、「 [Install Visual C++ for Cross-Platform Mobile Development](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)」を参照してください。 iOS 用のコードをビルドするには、Mac コンピューターと Apple iOS Developer アカウントも必要です。 詳細については、「 [iOS を使用してビルドするためのツールのインストールと構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。  
  
## <a name="come-up-to-speed"></a>最新情報を入手する  
 Android または iOS の開発者向けに開始方法を説明している優れた資料が用意されています。 Visual Studio は、表現力豊かな優れた開発環境です。 使用方法を学ぶには、「 [Android 開発者のための概要](https://msdn.microsoft.com/library/windows/apps/dn275875.aspx) 」または「 [iOS 開発者のための概要](https://msdn.microsoft.com/library/windows/apps/xaml/jj657966.aspx)」を参照してください。 これらのトピックでは、Visual Studio の概要と、Windows および Windows Phone 対応のクロスプラットフォーム アプリを開発する際に必要となる概念について紹介しています。 iOS および Android 用のクロスプラットフォーム アプリを初めて作成する場合は、「 [Build an OpenGL ES Application on Android and iOS](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)」を参照してください。  
  
 Visual C++ for Cross-Platform Mobile Development には、アプリの作成を開始する際に役立つ次のテンプレートが含まれています。  
  
- OpenGLES 2 アプリケーション (Android、iOS、Windows ユニバーサル)  
  
     Android Native Activity アプリ、iOS アプリ、およびユニバーサル Windows アプリをビルドするプロジェクトのセットと、C++ コードの共有ライブラリを含むソリューションを作成します。 これらのアプリでは、共通の C++ OpenGL ES コードを使用して作成されたプラットフォーム固有のライブラリを使用して、各アプリケーションで同じ回転する立方体を描画します。 このテンプレートを使用するには、Visual Studio をインストールするときに、[ユニバーサル Windows アプリ開発ツール] オプションを指定する必要があります。  
  
- Native-Activity アプリケーション (Android)  
  
     完全な C++ OpenGL アプリを Android Native Activity プロジェクトとして作成します。  
  
- OpenGLES アプリケーション (Android、iOS)  
  
     Android Native Activity アプリと iOS アプリの両方をビルドする一連のプロジェクトからなるソリューションを作成します。 これらのアプリでは、共通の C++ OpenGL ES コードを使用して作成されたプラットフォーム固有のライブラリを使用して、各アプリケーションで同じ回転する立方体を描画します。  
  
- 共有ライブラリ (Android、iOS)  
  
     共有プロジェクトで共通の C++ コードを使用して、Android ダイナミック ライブラリ (.so) ファイルと iOS スタティック ライブラリ (.a) ファイルを作成する複数のプロジェクトからなるソリューションを作成します。  
  
- 基本アプリケーション (Android、Ant)  
  
     Java ソース コードおよび Ant ビルド システムのみを使用する Android の「Hello, World」アプリ プロジェクトを作成します。  
  
- 基本アプリケーション (Android、Gradle)  
  
     Java ソース コードおよび Gradle ビルド システムのみを使用する Android の「Hello, World」アプリ プロジェクトを作成します。  
  
- 基本ライブラリ (Android、Ant)  
  
     Java ソース コードおよび Ant ビルド システムのみを使用する Android の「Hello, World」ライブラリ プロジェクトを作成します。  
  
- 基本ライブラリ (Android、Gradle)  
  
     Java ソース コードおよび Gradle ビルド システムのみを使用する Android の「Hello, World」ライブラリ プロジェクトを作成します。  
  
- ダイナミック共有ライブラリ (Android)  
  
     C++ コードを使用して、Android ダイナミック ライブラリ (.so) ファイルを作成します。  
  
- OpenGLES 2 アプリケーション (iOS)  
  
     OpenGL ES 2 iOS アプリをビルドするプロジェクトのセットを含むソリューションを作成します。 このアプリでは、OpenGL ES の C++ コードのライブラリを使用して、iOS アプリ内で回転するキューブを描画します。 このアプリは、iOS アプリに C++ のライブラリをインポートする方法を確認するための出発点として適しています。  
  
- スタティック ライブラリ (Android)  
  
     Android 用のスタティック ライブラリを構築するプロジェクトを作成します。 Android アプリでリンクできるダイナミック リンクは 1 つだけですが、スタティック ライブラリには数に制限なくリンクできます。  
  
- スタティック ライブラリ (iOS)  
  
     iOS 用のスタティック ライブラリを構築するプロジェクトを作成します。  
  
- メイクファイル プロジェクト (Android)  
  
     独自の Android メイクファイル プロジェクトのプロジェクト ラッパーを作成します。  
  
## <a name="try-out-sample-code"></a>サンプル コードを試す  
 Windows、Android、および iOS アプリで使用できる共有コード ライブラリを作成する方法、および Android の完全な Native Activity アプリを作成する方法を示すサンプルをダウンロードしてください。 作業を開始するには、「 [クロスプラットフォームモバイル開発の例](../cross-platform/cross-platform-mobile-development-examples.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
1. [Visual C++ for Cross-Platform Mobile Development のインストール](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)  
  
2. [IOS を使用してビルドするためのツールのインストールと構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)  
  
3. [Android Native Activity アプリの作成](../cross-platform/create-an-android-native-activity-app.md)  
  
4. [Android および iOS での OpenGL ES アプリケーションのビルド](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)  
  
5. [クロスプラットフォームモバイル開発の例](../cross-platform/cross-platform-mobile-development-examples.md)
