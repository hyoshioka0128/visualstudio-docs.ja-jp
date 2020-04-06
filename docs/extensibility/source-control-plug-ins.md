---
title: ソース管理プラグイン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cc5f092e0ae93109d071af0b1a67999947e73e90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699890"
---
# <a name="source-control-plug-ins"></a>ソース管理プラグイン
ソース管理プラグイン SDK リファレンス セクションには、ソース管理システムを と統合できるようにする完全なインターフェイス仕様[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]が含まれています。 このクラスは、統合開発環境 (IDE) とのインターフェイスを実装するためにソース管理プラグインが実装する必要がある、さまざまな[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]関数およびデータ型の構文とセマンティクスを指定します。

## <a name="in-this-section"></a>このセクションの内容
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)ソース管理プラグイン API に準拠するためにソース管理プラグインによって実装する必要がある関数を一覧表示します。

- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)特定のコマンドが実行されている間に、ソース管理プラグインが IDE に情報を返すために使用する機能について説明します。

- [列挙子](../extensibility/enumerators.md)ソース管理プラグインが知っている必要があるソース管理プラグイン API の列挙子データ型を一覧表示します。

- [機能フラグ](../extensibility/capability-flags.md)プロバイダーの機能`SCC_CAP_xxx`を示すフラグを記述します。

- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)特定のコマンドのコンテキストで役立つフラグをリストします。

- [エラー コード](../extensibility/error-codes.md)関数によって返される一般的なエラー`SCCTRN`値を として一覧表示します。

- [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)ソース管理プラグインを検索するためにレジストリにアクセスするためのキーについて説明します。

- [MSSCCPRJ.SCC ファイル](../extensibility/mssccprj-scc-file.md)IDE に対して不透明な情報を含むクライアント側のファイルを記述しますが、ソース管理プラグインがバージョン管理でソリューションまたはプロジェクトを検索するために使用します。

- [ソース管理プラグインの実装に関するベスト プラクティス](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)ソース管理プラグイン API の実装時に覚えておくべきことが重要な技術的な注意事項のコレクションを提供します。

- [文字列の長さの制限](../extensibility/restrictions-on-string-lengths.md)さまざまな関数で使用される文字列の長さに関するソース管理プラグイン API の制限事項について説明します。

- [用語集](../extensibility/source-control-plug-in-glossary.md)ソース管理プラグイン SDK ドキュメントを読むために役立つ用語とその定義を提供します。

- [方法 : ソース管理プラグインの互換性に関する警告をオフにする](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)警告を無効にする方法について説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインのサンプル](https://www.microsoft.com/download/details.aspx?id=55984)ソース管理プラグイン機能のサンプルを提供します。

- [ソース管理プラグインのテスト ガイド](../extensibility/internals/test-guide-for-source-control-plug-ins.md)ソース管理プラグインに関連するテスト手順について説明します。

- [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)ソース管理ユーザー インターフェイス (UI) を使用している間にソース管理機能を提供[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]するソース管理プラグインを作成する方法について説明します。

- [ビジュアル スタジオ SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)参照トピックの一覧を示します。
