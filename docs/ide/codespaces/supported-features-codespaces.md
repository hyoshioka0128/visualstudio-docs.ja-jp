---
title: サポートされている Visual Studio の機能 (プレビュー)
description: GitHub Codespaces を操作するときに使用できる Visual Studio IDE の機能について説明します。
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: f253ba9b7e46f809bc107aa2b3e26f635d778770
ms.sourcegitcommit: 754133c68ad841f7d7962e0b7a575e133289d8a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91928555"
---
# <a name="supported-visual-studio-features-preview"></a>サポートされている Visual Studio の機能 (プレビュー)

Visual Studio は、codespace に接続するときに豊富な開発エクスペリエンスを提供します。 使い慣れた Visual Studio の内部ループ ツールを使用して、ソース コードの編集、デバッグ、テスト、バージョン管理を行うことができます。また、プロジェクト テンプレート、リッチ コード ナビゲーション、IntelliSense などの生産性機能も利用できます。

現在の GitHub Codespaces の[パブリック ベータ版](https://github.com/features/codespaces)では、一部の Visual Studio 機能が完全にサポートされていないか、そもそも表示されない可能性があります。 以下のセクションでは、Visual Studio と GitHub Codespaces ベータ版で何ができるかと、今後見込まれる内容について説明します。 

ここには**すべての内容を記載しません**が、codespace に接続されている場合の、Visual Studio の全般的な機能について説明しています。

> [!NOTE]
> codespace を Visual Studio と共に使用しているときの機能で不足しているものがある場合は、 https://developercommunity.visualstudio.com/ からイシューを作成してお知らせください。 これにより、特に必要な機能の優先度付けができるようになります。

> [!NOTE]
> 次に示す機能は Visual Studio 用であり、他の 2 つの GitHub Codespaces クライアント (Visual Studio Code とブラウザー内エディター) には対応していません。

## <a name="edit-and-navigation"></a>編集とナビゲーション

IntelliSense、コードのナビゲーション、診断、提案などのスマート言語機能を利用できるため、codespace でのソース コードの編集には、ほとんど違いがありません。

* IntelliSense*
* コードのナビゲーション*
* [ドキュメントのフォーマット] でのコードの書式設定
* 構文の強調表示
* クイック ヒント*
* HTML、CSS、Razor エディター* - 部分的なサポート。
* JavaScript および TypeScript エディター* - 部分的なサポート。

まだ使用不可能:

* IntelliSense* - オートコンプリート/メンバー一覧フィルターの一部が使用できません。 インポートされていない型と [ウォッチ] ウィンドウの IntelliSense の入力候補はまだ使用できません。
* コード ナビゲーション* - ほとんどのコマンドがサポートされています。 パスの指定による [基本へ移動] および [複数のファイル内を検索] は、まだサポートされていません。
* クイック ヒント* - クイック ヒントの色付けはサポートされていません。
* HTML、CSS、Razor エディター* - 診断、IntelliSense 入力候補、クイック ヒント、スマート インデント。 現在、セマンティックの色付け、ナビゲーション コマンドなどはサポートされていません。
* JavaScript および TypeScript エディター* - スクリプト ブロック (たとえば、HTML と CSHTML ファイルの JavaScript コンテンツ) とセマンティックの強調表示はまだサポートされていません。 既知のイシューでの電球の機能とリンティング。
* CMake ターゲット ビュー
* CMake プロジェクト設定エディター
* Ctrl + F7 (ファイルのコンパイル)
* CodeLens
* コード スニペット
* IntelliCode

## <a name="application-types-and-configuration"></a>アプリケーションの種類と設定

ほとんどのアプリケーションの種類とプロジェクトの構成がサポートされていますが、ビジュアル デザイナーを使用せずにプロジェクト コードを直接編集する必要があります。 構成のガイダンスは、「[codespace をカスタマイズする方法](customize-codespaces.md)」を参照してください。

* プロジェクト テンプレートと項目テンプレート
* .NET Core と ASP.NET Core のプロジェクト
* C++ コンソール アプリ - CMake と .vcxproj がサポートされています
* Linux をターゲットとする C++ アプリ - ほとんどは GUI 以外でサポートされています。 WSL、プラットフォーム固有の IntelliSense、およびビルドをインストールしてプロビジョニングする機能。
* プロジェクト ファイルの編集 - ほとんどがサポートされています。 一部の入力候補、構文の強調表示、高度な編集機能が不足しています。
* GitHub アカウント - Codespaces を作成して接続し、GitHub のアカウントで利用可能なリソースにアクセスするために使用できます。
* Azure CLI - サインインした Visual Studio ID またはキーチェーン アカウントは共有しません。 ブラウザーベースのログインはサポートされていませんが、`az login --use-device-code` を使用して、統合ターミナル内で認証できます。

まだ使用不可能:

* UI デザイナー - WinForms、WPF、およびリソース デザイナー
* Visual Basic および F# のプロジェクト
* .NET Framework をターゲットとするプロジェクト
* Docker Compose プロジェクト
* [プロジェクト プロパティ] ページ
* ASP.NET Core テンプレートの認証オプション
* インストールのために GUI が必要なアプリ - ターミナルと共にインストールできるものはすべてサポートされています (chocolatey インストーラーを含む) が、実際の GUI はすぐには使用できません。 現在の回避策として、GUI にアクセスするための全画面 Live Share を有効にしてください。 管理コンソールにはアクセスできません。 インストールのために再起動が必要なアプリはサポートされていません。
* Visual Studio の Azure リソースのマネージド ID
* イントラネット リソース (プライベート ネットワーク) - 現時点で、codespace は VPN を必要とするリソースに接続できません。
* 拡張機能 - Visual Studio で Codespaces を使用する場合、拡張機能はサポートされません。

## <a name="debugging"></a>デバッグ

ブレークポイントの設定、基本的なステップ イン コード、変数の検査、[ローカル]、[自動変数]、[ウォッチ] のウィンドウなど、基本的な内部ループ デバッグがサポートされています。 追加のウィンドウ、カスタマイズ、ビジュアライザーの一部はサポートされていません。

* ブレークポイント*
* 基本的なステップ
* [ローカル]、[自動変数]、[ウォッチ] ウィンドウ* - 部分的なサポート。
* シンボル サーバー、ソース サーバー、およびデータのインポート/エクスポートのヒントは、すべて部分的にサポートされています。

まだ使用不可能:

* ブレークポイント* - ブレークポイントのラベル、データ ブレークポイント、および [逆アセンブリ] ウィンドウのブレークポイントの設定が進行中です。 ブレークポイントのインポートとエクスポートは部分的にサポートされています。
* [ローカル]、[自動変数]、[ウォッチ] ウィンドウ* - 検索ボックスおよび検索ボックス ナビゲーションでのステートメント入力候補などの一部の機能。
* UI のカスタマイズ - ピン留め可能なプロパティとテンプレート パラメーターの非表示はサポートされていません。
* ビジュアライザー - C++ natvis が部分的にサポートされています。 [逆アセンブリ] ウィンドウ、XAML ビジュアル診断、カスタム .NET ビジュアライザー、データセット ビジュアライザーはサポートされていません。
* 追加のデバッガー ウィンドウ - [プロセス] ウィンドウは部分的にサポートされています。 [並列スタック] ウィンドウ - [タスク] ビュー、診断ハブ、ソースとシンボルの検索ダイアログはサポートされていません。
* 一部のデバッガー ワークフロー - プロセスにアタッチ、Just-In-Time (JIT) デバッガー、ダンプ デバッグ、プロファイル、IntelliTrace はサポートされていません。 C++ の [マイコードのみ] のステップ実行は部分的にサポートされています。
* エディット コンティニュ - マネージド コードとネイティブ コードの両方でサポートされていません。
* スレッド機能 - スレッドの凍結/凍結解除、スレッド名の変更、ソース内のスレッドの表示はサポートされていません。
* その他のステップ実行機能 - プロパティと演算子 (.NET Core) の自動ステップ オーバーと [関数にステップ イン] はサポートされていません。 

## <a name="features"></a>特徴

codespace に接続されている Visual Studio を使用する場合、ローカルで作業する場合と同じユーザー補助機能を利用できます。

* ソース管理 - 新しい [Git ウィンドウ](https://devblogs.microsoft.com/visualstudio/improved-git-experience-in-visual-studio-2019/)では、Git が完全にサポートされています。
* アクセシビリティ - デバッグ対象のアプリの appcasting にアクセスできない支援技術の既知のイシューが 1 つあります。 この制限に加えて、ローカルの Visual Studio エクスペリエンスにまだ存在しない他の互換性のイシューがあるとは考えていません。 バグを見つけた場合は、[Developer Community](https://developercommunity.visualstudio.com/) にイシューを提出してお知らせください。
* 発行 - GitHub Actions では [Azure に発行する] がサポートされています。
* 接続済みサービス - App Insights、KeyVault、Storage、SQL、Redis、Cosmos、OpenAPI、gRPC は部分的にサポートされています。
* テスト エクスプローラー* - ほとんどがサポートされています。

まだ使用不可能:

* テスト エクスプローラー* - 既定のアーキテクチャの選択、テストの並列実行、プレイリストなどの一部の機能。単体テスト、実行設定、およびいくつかの追加のエンタープライズ機能のデバッグに関する既知のイシュー。 単体テストのプロファイルはサポートされていません。
* NuGet パッケージ マネージャー UI - NuGet コマンド ラインがサポートされています。
* エンタープライズ テスト機能 - Live Unit Testing、Microsoft Fakes、コード カバレッジ、IntelliTest はサポートされていません。
* 高度な発行シナリオ: 選択的発行、FTP 発行、変更のプレビュー、クイック発行ツール バーなど。

## <a name="see-also"></a>関連項目

* [GitHub Codespaces とは](codespaces-overview.md)
* [codespace で Visual Studio を使用する方法](use-visual-studio-with-codespaces.md)
* [codespace をカスタマイズする方法](customize-codespaces.md)
