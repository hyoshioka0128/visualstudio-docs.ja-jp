---
title: クロスプラットフォームの C++ によるモバイル開発 | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 0bb872d6-981b-4c96-9143-fcec5336bf0d
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: bc4164ec405aed2941e807934ee8d66b7ae72504
ms.sourcegitcommit: ca3bb6db949f5e405f6ffe1afa5f430662c1173f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2019
ms.locfileid: "74098981"
---
# <a name="cross-platform-mobile-development-with-c"></a>C++ によるクロスプラットフォーム モバイル開発

Visual Studio で利用可能なクロスプラットフォーム ツールを使用して、iOS、Android、Windows デバイス用のネイティブ C++ アプリをビルドできます。 **C++ によるモバイル開発**は、Visual Studio インストーラーで使用できるワークロードです。 それでは、共有ライブラリとネイティブ アプリのクロスプラットフォーム開発に必要な SDK とツールがインストールされます。 インストールされている場合、iOS と Android のデバイスおよびプラットフォーム、Windows、Windows Store、Xbox で実行されるコードを、C++ を使用して作成できます。

複数のプラットフォーム用にコードを記述することは、ストレスのたまる作業になることがよくあります。 iOS、Android、および Windows の主要な開発言語とツールは、それぞれのプラットフォームによって異なります。 ただし、すべてのプラットフォームは共通して C++ コードの記述をサポートしています。 それは、プラットフォーム間でのコア コードの再利用を可能にできる共通項です。 C++ で記述されたネイティブ コードは、パフォーマンスに優れているだけでなく、リバース エンジニアリングに対する耐性もあります。 コードを再利用できれば、複数のプラットフォーム用にアプリを作成する場合にかかる時間と労力の両方を節約できます。

クロスプラットフォーム モバイル開発用の C++ を使用する開発には、次の利点があります。

- **インストールが簡単。** Visual Studio インストーラーによって、Android と iOS のアプリまたはライブラリを作成するために必要となるサード パーティ製のツールと SDK が取得され、インストールされます。 構成とセットアップは単純で、ほとんどが自動的に行われます。

- **強力で使い慣れたビルド環境。** Visual Studio テンプレートを使用して、共有可能なクロスプラットフォーム ソリューションおよびプロジェクトを簡単に作成できます。 1 つの共通インターフェイスを使用して、すべてのプロジェクトのプロパティを管理できます。 すべてのコードを Visual Studio エディターで編集できるため、組み込みのクロスプラットフォーム IntelliSense のコード補完機能とエラーの強調表示を利用できます。

- **統合されたデバッグ操作。** Visual Studio のワールドクラスのデバッグ ツールを使用して、次のようなすべてのプラットフォームで C++ コードを観察しながらステップ実行できます: Android のデバイスとエミュレーター、iOS のシミュレーターとデバイス、Windows または Windows Store のデバイスとエミュレーター。

## <a name="get-the-tools"></a>ツールを取得する

C++ によるモバイル開発は、Visual Studio に付属しているインストール可能なワークロードです。 前提条件とインストール手順については、「[C++ によるクロスプラットフォーム モバイル開発をインストールする](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)」を参照してください。 iOS 用のコードをビルドするには、Mac コンピューターと Apple iOS Developer アカウントも必要です。 詳細については、「[iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。

## <a name="come-up-to-speed"></a>最新情報を入手する

Android または iOS の開発者向けに開始方法を説明している優れた資料が用意されています。 Visual Studio は、表現力豊かな優れた開発環境です。 使用方法を学ぶには、「[Android 開発者のための概要](/previous-versions/windows/apps/dn275875\(v=win.10\))」または「[iOS 開発者のための概要](/previous-versions/windows/apps/jj657966\(v=win.10\))」を参照してください。 これらの記事では、Visual Studio の概要と、Windows および Windows Store 対応のクロスプラットフォーム アプリを開発するときに必要となる概念について紹介しています。 iOS および Android 用のクロスプラットフォーム アプリを初めて作成する場合は、「[Android および iOS での OpenGL ES アプリケーションのビルド](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)」を参照してください。

C++ によるモバイル開発ワークロードには、アプリの作成を始めるときに役立つ次のテンプレートが含まれています。

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

Windows、Android、および iOS アプリで使用できる共有コード ライブラリの作成方法がわかるサンプルをダウンロードします。 そして、Android 用の完全な Native Activity アプリを作成する方法を確認します。 開始するには、「[クロス プラットフォーム モバイル開発の例](../cross-platform/cross-platform-mobile-development-examples.md)」を参照してください。

## <a name="see-also"></a>関連項目

[C++ によるクロスプラットフォーム モバイル開発をインストールする](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)\
[iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)\
[Android Native Activity アプリを作成する](../cross-platform/create-an-android-native-activity-app.md)\
[Android および iOS での OpenGL ES アプリケーションのビルド](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)\
[クロス プラットフォーム モバイル開発の例](../cross-platform/cross-platform-mobile-development-examples.md)
