---
title: ソース管理プラグイン |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a5a99ebdf2366ce6a60a6a724afc7d742db7150f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65705802"
---
# <a name="source-control-plug-ins"></a>ソース管理プラグイン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソース管理プラグイン SDK リファレンスセクションには、ソース管理システムをと統合できるようにするための完全なインターフェイス仕様が含まれてい [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 これは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 統合開発環境 (IDE: integrated development environment) とのインターフェイスとして、ソース管理プラグインが実装する必要のあるさまざまな関数とデータ型の構文とセマンティクスを指定します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)  
 ソース管理プラグイン API に準拠するためにソース管理プラグインによって実装される必要がある関数の一覧を示します。  
  
 [IDE で実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)  
 特定のコマンドが実行されている間に、ソース管理プラグインが IDE に情報を返すために使用する関数について説明します。  
  
 [列挙子](../extensibility/enumerators.md)  
 ソース管理プラグインが認識する必要があるソース管理プラグイン API 内の列挙子データ型を一覧表示します。  
  
 [機能フラグ](../extensibility/capability-flags.md)  
 `SCC_CAP_xxx`プロバイダーの機能を示すフラグについて説明します。  
  
 [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)  
 特定のコマンドのコンテキストで役に立つフラグの一覧を示します。  
  
 [エラー コード](../extensibility/error-codes.md)  
 関数によって返される一般的なエラー値をとして一覧表示 `SCCTRN` します。  
  
 [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)  
 ソース管理プラグインを検索するためにレジストリにアクセスするためのキーについて説明します。  
  
 [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)  
 IDE に対して不透明な情報が含まれているクライアント側のファイルを記述します。これは、ソース管理プラグインによって、バージョン管理でソリューションまたはプロジェクトを検索するために使用されます。  
  
 [ソース管理プラグインを実装するためのベスト プラクティス](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)  
 ソース管理プラグイン API の実装中に覚えておく必要がある重要なテクニカルリマインダーのコレクションを提供します。  
  
 [文字列長の制限](../extensibility/restrictions-on-string-lengths.md)  
 さまざまな関数で使用される文字列の長さに対するソース管理プラグイン API の制限事項について説明します。  
  
 [用語集](../extensibility/source-control-plug-in-glossary.md)  
 ソース管理プラグイン SDK ドキュメントを読むための便利な用語とその定義を提供します。  
  
 [方法: ソース管理プラグインの互換性に関する警告をオフにする](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)  
 警告を無効にする方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ソース管理プラグインのサンプル](https://msdn.microsoft.com/61de7d2b-71db-451e-8e3e-d41b11c7a4ca)  
 ソース管理プラグインの機能のサンプルを提供します。  
  
 [ソース管理プラグイン向けのテスト ガイド](../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 ソース管理プラグインに関連するテスト手順について説明します。  
  
 [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)  
 ソース管理の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ユーザーインターフェイス (UI) を使用しているときにソース管理機能を提供するソース管理プラグインを作成する方法について説明します。  
  
 [Visual Studio SDK のリファレンス](../extensibility/visual-studio-sdk-reference.md)  
 参照トピックの一覧を示します。
