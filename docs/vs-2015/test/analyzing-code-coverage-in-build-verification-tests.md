---
title: ビルド確認テストのコード カバレッジの分析 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 59c07d15-511e-4fd0-b398-bde9d5ed00d9
caps.latest.revision: 10
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2442bf4cc31eeb51332aa28325924e18ccb1ffb7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660728"
---
# <a name="analyzing-code-coverage-in-build-verification-tests"></a>ビルド確認テストのコード カバレッジの分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft Visual Studio のコード カバレッジ分析は、コードの中で自動テストで実行されている割合を示します。 詳細については、「[コード カバレッジを使用した、テストされるプロジェクトのコード割合の確認](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)」を参照してください。

 コードをチェックインすると、テストがビルド サーバー上で、他のチーム メンバーによる他のすべてのテストと共に実行されます。 (まだ設定していない場合は、「 [ビルドプロセスでのテストの実行](https://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38)」を参照してください)。ビルドサービスでコードカバレッジを分析すると便利です。これは、プロジェクト全体のカバレッジを最新で包括的に把握できるようにするためです。 これには、自動化されたシステム テストと、通常は開発用コンピューターでは実行しない、その他のコード化されたテストも含まれます。

1. チーム エクスプローラーで、[**ビルド**] を開き、ビルド定義を追加または編集します。

2. [**プロセス**] ページで [**自動テスト**]、[**テスト ソース**]、[**実行設定**] の順に展開します。 [**実行設定の種類**] を [**コード カバレッジの有効化**] に設定します。

    複数のテスト ソース定義がある場合は、各定義に対してこの手順を繰り返します。

   - <em>ただし、* "*実行設定ファイルの種類</em>" という名前のフィールドはありません*。 *

      [**自動テスト**] の下の [**テスト アセンブリ**] を選択し、行の末尾の省略記号 (**[...]**) ボタンを選択します。 [**テストの実行の追加と編集**] ダイアログ ボックスで、[**テスト ランナー**] の下の [**Visual Studio テスト ランナー**] を選択します。

   ![コード カバレッジのビルド定義の設定](../test/media/codecoverage-plaincc.png "CodeCoverage-plainCC")

   ビルドの実行後、コード カバレッジの結果がビルドの概要に表示されます。

## <a name="see-also"></a>参照
 [コード カバレッジを使用した、テストされるプロジェクトのコード割合の確認](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)
