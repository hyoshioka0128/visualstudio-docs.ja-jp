---
title: ソース管理プラグイン |Microsoft Docs
description: このセクションの記事では、ソース管理システムを Visual Studio と統合できるようにするための完全なインターフェイス仕様について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 617b06e46bb150026f49af3e23761dfd6cb4e902
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715835"
---
# <a name="source-control-plug-ins"></a>ソース管理プラグイン
ソース管理プラグイン SDK リファレンスセクションには、ソース管理システムをと統合できるようにするための完全なインターフェイス仕様が含まれてい [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 これは、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) とのインターフェイスとして、ソース管理プラグインが実装する必要のあるさまざまな関数とデータ型の構文とセマンティクスを指定します。

## <a name="in-this-section"></a>このセクションの内容
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md) ソース管理プラグイン API に準拠するためにソース管理プラグインによって実装される必要がある関数の一覧を示します。

- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md) 特定のコマンドが実行されている間に、ソース管理プラグインが IDE に情報を返すために使用する関数について説明します。

- [列挙子](../extensibility/enumerators.md) ソース管理プラグインが認識する必要があるソース管理プラグイン API 内の列挙子データ型を一覧表示します。

- [機能フラグ](../extensibility/capability-flags.md)`SCC_CAP_xxx`プロバイダーの機能を示すフラグについて説明します。

- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md) 特定のコマンドのコンテキストで役に立つフラグの一覧を示します。

- [エラーコード](../extensibility/error-codes.md) 関数によって返される一般的なエラー値をとして一覧表示 `SCCTRN` します。

- [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md) ソース管理プラグインを検索するためにレジストリにアクセスするためのキーについて説明します。

- [Mssccprj.scc。SCC ファイル](../extensibility/mssccprj-scc-file.md) は、IDE に対して不透明な情報を含むクライアント側のファイルを記述しますが、ソース管理プラグインによって、バージョン管理でソリューションまたはプロジェクトを検索するために使用されます。

- [ソース管理プラグインを実装するためのベストプラクティス](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md) ソース管理プラグイン API の実装中に覚えておく必要がある重要なテクニカルリマインダーのコレクションを提供します。

- [文字列の長さに関する制限](../extensibility/restrictions-on-string-lengths.md) さまざまな関数で使用される文字列の長さに対するソース管理プラグイン API の制限事項について説明します。

- [用語集](../extensibility/source-control-plug-in-glossary.md) ソース管理プラグイン SDK ドキュメントを読むための便利な用語とその定義を提供します。

- [方法: ソース管理プラグインの互換性に関する警告をオフにする](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md) 警告を無効にする方法について説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインのサンプル](https://www.microsoft.com/download/details.aspx?id=55984) ソース管理プラグインの機能のサンプルを提供します。

- [ソース管理プラグインのテストガイド](../extensibility/internals/test-guide-for-source-control-plug-ins.md) ソース管理プラグインに関連するテスト手順について説明します。

- [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md) ソース管理の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ユーザーインターフェイス (UI) を使用しているときにソース管理機能を提供するソース管理プラグインを作成する方法について説明します。

- [Visual STUDIO SDK リファレンス](../extensibility/visual-studio-sdk-reference.md) 参照トピックの一覧を示します。
