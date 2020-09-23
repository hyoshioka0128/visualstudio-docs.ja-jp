---
title: 'Visual Studio のドキュメント:新機能の履歴 '
titleSuffix: ''
description: Visual Studio ドキュメントの新機能に関する履歴
ms.date: 09/01/2020
helpviewer_keywords:
- Visual Studio, what's new, docs
- what's new [Visual Studio]
ms.assetid: 511DAFC7-896E-449A-BFF7-0E8F7BBA8A78
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 8505f98163c57fe276bcf4c76195fe843300394f
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809467"
---
# <a name="history-of-whats-new-in-visual-studio-docs"></a>Visual Studio ドキュメントの新機能に関する履歴

Visual Studio ドキュメントの新機能に関する履歴へようこそ。このトピックには、2020 年 8 月より前 (2020 年 7 月以降) のドキュメントに対する主な変更点が含まれます。 最新の新機能については、[Visual Studio の最新情報](whats-new-visual-studio-docs.md)に関するドキュメントを参照してください。

## <a name="july-2020"></a>2020 年 7 月
### <a name="code-quality"></a>コード品質

**新しい記事**

- [CA1417:P/Invoke の文字列パラメーターに `OutAttribute` を使用しない](../code-quality/ca1417.md) - CA1417 のドキュメントを追加
- [CA1805:不必要に初期化しない。](../code-quality/ca1805.md) - CA1805 のドキュメントを追加
- [CA1836:使用可能な場合は、Count よりも IsEmpty を優先します](../code-quality/ca1836.md) - CA1836 の記事を追加 (Count よりも IsEmpty を優先します)
- [CA2016:CancellationToken パラメーターを 1 つのメソッドに転送する](../code-quality/ca2016.md) - ドキュメント CA2016 - CancellationToken パラメーターを 1 つのメソッドに転送する
- [CA2350:DataTable.ReadXml() の入力が信頼されていることを確認してください](../code-quality/ca2350.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2351:DataSet.ReadXml() の入力が信頼されていることを確認してください](../code-quality/ca2351.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2352:シリアル化可能な型の安全でない DataSet または DataTable は、リモート コード実行攻撃に対して脆弱になる可能性があります](../code-quality/ca2352.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2353:シリアル化可能な型の安全でない DataSet または DataTable](../code-quality/ca2353.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2354:逆シリアル化されたオブジェクト グラフの安全でない DataSet または DataTable は、リモート コード実行攻撃に対して脆弱になる可能性があります](../code-quality/ca2354.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2355:逆シリアル化されたオブジェクト グラフの安全でない DataSet または DataTable](../code-quality/ca2355.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2356:Web の逆シリアル化されたオブジェクト グラフの安全でない DataSet または DataTable 型](../code-quality/ca2356.md) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント

### <a name="containers"></a>コンテナー

**新しい記事**

- [Local Process with Kubernetes を構成する](../containers/configure-local-process-with-kubernetes.md) - Local Process with Kubernetes: yaml の構成
- [Local Process with Kubernetes (プレビュー) の使用](../containers/local-process-kubernetes.md) - 開発スペースの移行
- [Local Process with Kubernetes のしくみ](../containers/overview-local-process-kubernetes.md)
  - Local Process for Kubernetes:ルーティング セクションの追加
  - 開発スペースの移行

### <a name="cross-platform"></a>クロス プラットフォーム

**更新された記事**

- [変更ログ (Visual Studio Tools for Unity、Windows)](../cross-platform/change-log-visual-studio-tools-for-unity.md) - Bump VSTU 変更ログ 4.7.1.0
- [変更ログ (Visual Studio Tools for Unity、Mac)](../cross-platform/change-log-visual-studio-tools-for-unity-mac.md) - Bump VSTUM 変更ログ 2.7.1.0

### <a name="get-started"></a>はじめに

**新しい記事**

- [チュートリアル: シンプルな C# コンソール アプリを拡張する](../get-started/csharp/tutorial-console-part-2.md) - 拡張路上チュートリアルの最初のバージョンをリリース

### <a name="ide"></a>IDE

**新しい記事**

- [Developer Community のガイドライン](./developer-community-guidelines.md) - DevCom ガイドラインを追加
- [インポートされていない型と拡張メソッドに対する IntelliSense 入力候補](./reference/intellisense-completion-unimported-types-extension-methods.md)

### <a name="install"></a>インストール

**新しい記事**

- [最小限のオフライン レイアウトを使用して Visual Studio を更新する](../install/update-minimal-layout.md) - 最小限のレイアウト機能に関するドキュメント
- [Visual Studio 企業向けガイド](../install/visual-studio-enterprise-guide.md) - 企業向けガイド

### <a name="javascript"></a>JavaScript

**新しい記事**

- [TypeScript コードのコンパイル (Node.js)](../javascript/compile-typescript-code-npm.md) - TypeScript のコンパイルとビルド
- [TypeScript コードのコンパイル (ASP.NET Core)](../javascript/compile-typescript-code-nuget.md) - TypeScript のコンパイルとビルド

### <a name="msbuild"></a>MSBuild

**新しい記事**

- [一般的な MSBuild 項目メタデータ](../msbuild/common-msbuild-item-metadata.md) - MSBuild: Link と LinkBase の省略可能なメタデータに関する表を追加
- [MSBuild でのソリューション フィルター](../msbuild/solution-filters.md) - MSBuild のソリューション フィルター

### <a name="test"></a>テスト

**新しい記事**

- [テスト エクスプローラーを使用した単体テストのデバッグと分析](../test/debug-unit-tests-with-test-explorer.md) - テスト エクスプローラーのパフォーマンス作業

**更新された記事**

- [ *.runsettings* ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
  - runsettings ファイルを使用した単体テストの構成に関する更新
  - Blame オプションの説明が変更され、例が追加されました。