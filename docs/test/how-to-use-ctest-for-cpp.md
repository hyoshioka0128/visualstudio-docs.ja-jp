---
title: C++ 用の CTest を使用する方法
description: 既定で Visual Studio IDE に統合されている CTest を使用して、テストを作成および実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/23/2020
ms.topic: how-to
ms.author: corob
manager: jmartens
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 23d235d4b18c9909868cf890e31d835b3f7ea948
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969283"
---
# <a name="how-to-use-ctest-for-c-in-visual-studio-2017-and-later"></a>Visual Studio 2017 以降で C++ 用の CTest を使用する方法

CMake (CTest を含む) は、**C++ によるデスクトップ開発** ワークロードのコンポーネントとして Visual Studio IDE に既定で統合されています。 それをご自分のコンピューターにインストールする必要がある場合、Visual Studio Installer プログラムを開き、**[C++ によるデスクトップ開発]** ボタンをクリックし、**[変更]** をクリックします。 ワークロード コンポーネントの一覧で **[Windows 用 C++ CMake ツール]** を選択します。

## <a name="to-write-tests"></a>テストを記述するには

Visual Studio の CMake サポートでは、Visual Studio プロジェクト システムを必要としません。 したがって、任意の CMake 環境の場合と同様に、CTest テストを記述して構成します。 `enable_testing()` コマンドを使用してテストを有効にし、`add_test()` コマンドまたは `gtest_discover_tests()` コマンドを使用して新しいテストを追加します。 CTest の詳細については、[CMake のドキュメント](https://gitlab.kitware.com/cmake/community/wikis/doc/ctest/Testing-With-CTest)を参照してください。 

Visual Studio での CMake 使用について詳しくは、「[Visual Studio の CMake プロジェクト](/cpp/build/cmake-projects-in-visual-studio)」をご覧ください。

## <a name="to-run-tests"></a>テストを実行するには

CTest は **テスト エクスプローラー** に完全に統合され、Google 単体テスト フレームワークと Boost 単体テスト フレームワークの両方もサポートしています。 これらのフレームワークは、**C++ によるデスクトップ開発** ワークロードにコンポーネントとして既定で含まれています。 ただし、Visual Studio の以前のバージョンからプロジェクトをアップグレードする場合は、Visual Studio インストーラー プログラムを使用してこれらのフレームワークをインストールする必要があります。

次の図は、Google テスト フレームワークを使用して実行した CTest の結果を示しています。

![Visual Studio での Google Test Framework による CTest](media/ctest-test-explorer.png)

CTest を使用するが、Google アダプターまたは Boost アダプターを使用していない場合、結果は、個別のテスト方法レベルではなく、CTest レベルで表示されます。 CTest 専用実行可能ファイルのデバッグとステップ実行を行うことができますが、個々のテストのスタック トレースはサポートされません。

## <a name="see-also"></a>関連項目

- [C/C++ 用の単体テストの記述](writing-unit-tests-for-c-cpp.md)
