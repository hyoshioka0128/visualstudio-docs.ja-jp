---
title: コード分析のアプリケーション エラー
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio ALM], code analysis
- code analysis, errors
- managed code, code analysis errors
- code analysis, policy errors
ms.assetid: d8fd9475-ac9b-4085-b5a3-b0c807922cac
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ef5ccc0cf432a5c6782b76c4623bfdc55f66a8b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538556"
---
# <a name="code-analysis-application-errors"></a>コード分析のアプリケーション エラー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
このセクションでは、マネージコード分析ツールによって生成されるエラーメッセージのリファレンスを示します。 特定のエラーメッセージのヘルプを表示するには、インデックスの [ **検索対象** ] ボックスにエラー番号を入力します。

## <a name="in-this-section"></a>このセクションの内容

|Item|値|
|-|-|
|[CA0001](ca0001.md)|マネージコード分析ツール内で、予期されたエラー条件を示していない例外が発生しました。|
|[CA0051](ca0051.md)|ルールが選択されていません。|
|[CA0052](ca0052.md)|分析するターゲットが選択されていません。|
|[CA0053](ca0053.md)|規則アセンブリを読み込むことができませんでした。|
|[CA0054](ca0054.md)|カスタム規則アセンブリに無効な XML リソースが含まれています。|
|[CA0055](ca0055.md)|ファイルを読み込めませんでした:\<path>|
|[CA0056](ca0056.md)|プロジェクトファイルの分析ツールのバージョンが正しくありません。|
|[CA0057](ca0057.md)|現在のターゲットとルールのセットに違反をマップすることはできません。|
|[CA0058](ca0058.md)|参照されたアセンブリを読み込めません。|
|[CA0059](ca0059.md)|コマンドラインスイッチエラー。|
|[CA0060](ca0060.md)|間接的に参照されたアセンブリを読み込むことができません。|
|[CA0061](ca0061.md)|ルール '*RuleId*' が見つかりませんでした。|
|[CA0062](ca0062.md)|ルールセット '*RuleSetName*' で参照されているルール '*RuleId*' が見つかりませんでした。|
|[CA0063](ca0063.md)|規則セットファイルまたはその依存する規則セットファイルの1つを読み込むことができませんでした。|
|[CA0064](ca0064.md)|指定された規則セットに FxCop 規則が含まれていなかったため、分析は実行されませんでした。|
|[CA0065](ca0065.md)|サポートされていないメタデータコンストラクトです: 型 '*TypeName*' には、'*propertyfieldname*' という同じ名前のプロパティとフィールドの両方が含まれています|
|[CA0066](ca0066.md)|**/Targetframeworkversion**に指定された値 '*VersionID*' は、認識されているバージョンではありません。|
|[CA0067](ca0067.md)|ディレクトリが見つかりません。|
|[CA0068](ca0068.md)|ターゲットアセンブリ *' AssemblyName '* のデバッグ情報が見つかりませんでした。|
|[CA0069](ca0069.md)|代替プラットフォームを使用しています。 *FrameworkVersion1* が見つかりませんでした。 代わりに *FrameworkVersion2* を使用してください。 最適な分析結果を得るには、正しい .NET Framework がインストールされていることを確認してください。|
|[CA0070](ca0070.md)|セキュリティのアクセス許可により、アセンブリまたは型を読み込むことができません。|
|[CA0501](ca0501.md)|出力レポートを読み取れません。|
|[CA0502](ca0502.md)|サポートされていない言語です。|
|[CA0503](ca0503.md)|プロパティは非推奨とされます。 Superceding プロパティを使用する|
|[CA0504](ca0504.md)|規則ディレクトリは存在しないため、無視されました|
|[CA0505](ca0505.md)|プロパティは非推奨とされます。 Superceding プロパティを使用する|
|[FxCopCmd エラー](fxcopcmd-errors.md)|マネージコード分析エラー。|

## <a name="related-sections"></a>関連項目

- [安全なコードを記述するためのガイドライン](https://msdn.microsoft.com/9892fd19-45cd-44b6-9fa8-10f1b5cb6ea4)
- [マネージド コードの品質の分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)
- [アプリケーション ライフサイクル管理ツールにおけるエラーのトラブルシューティングに関するリソース](https://msdn.microsoft.com/library/76ca8f76-1e2d-4b55-89e2-bd59e4abe74c)