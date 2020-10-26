---
title: ソース管理プラグインのテストガイド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control [Visual Studio SDK], testing plug-ins
- tests, source control plug-ins
- testing, source control plug-ins
- source control plug-ins, test guide
ms.assetid: 13b74765-0b7c-418e-8cd9-5f2e8db51ae5
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6790e61eddc81045bb168028ee7aeef7a0492e3c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825741"
---
# <a name="test-guide-for-source-control-plug-ins"></a>ソース管理プラグイン向けのテスト ガイド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このセクションでは、を使用したソース管理プラグインのテストに関するガイダンスを提供 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。 最も一般的なテスト領域の概要と、問題がある可能性がある複雑な領域の一部を紹介します。 この概要は、テストケースの完全な一覧ではありません。  
  
> [!NOTE]
> 以前 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のバージョンのを使用しているときに以前に検出されなかった既存のソース管理プラグインに関する問題は、最新の IDE のバグ修正および機能強化によって発見される可能性があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 以前のバージョンの以降、プラグインに変更が加えられていない場合でも、このセクションで列挙されている領域については、既存のソース管理プラグインをテストすることを強くお勧めし [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="common-preparation"></a>一般的な準備  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]とターゲットソース管理プラグインがインストールされているコンピューターが必要です。 同様に構成された2つ目のコンピューターは、オープンソース管理テストの一部で使用できます。  
  
## <a name="definition-of-terms"></a>用語の定義  
 このテストガイドでは、次の用語定義を使用します。  
  
 クライアントプロジェクト  
 ソース管理の統合をサポートするで使用できるプロジェクトの種類 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ( [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 、、など [!INCLUDE[csprcs](../../includes/csprcs-md.md)] [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] )。  
  
 Web プロジェクト (Web project)  
 Web プロジェクトには、ファイルシステム、ローカル IIS、リモートサイト、および FTP の4種類があります。  
  
- ファイルシステムプロジェクトはローカルパスに作成されますが、UNC パスを使用して内部でアクセスされるため、インターネットインフォメーションサービス (IIS) をインストールする必要はありません。また、クライアントプロジェクトと同様に、IDE 内からソース管理下に配置することもできます。  
  
- ローカル IIS プロジェクトは、同じコンピューターにインストールされ、ローカルコンピューターを指す URL を使用してアクセスされる IIS で動作します。  
  
- リモートサイトプロジェクトは IIS サービスでも作成されますが、IDE 内からではなく、IIS サーバーコンピューターのソース管理下に配置され [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
- FTP プロジェクトはリモート FTP サーバーを介してアクセスされますが、ソース管理下に配置することはできません。  
  
  参加  
  ソリューションまたはプロジェクトのソース管理下にあるもう1つの用語。  
  
  バージョンストア  
  ソース管理プラグイン API を使用してアクセスされているソース管理データベース。  
  
## <a name="test-areas-covered-in-this-section"></a>このセクションで説明されているテスト領域  
  
- [テスト領域 1: ソース管理への追加とオープン](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)  
  
  - ケース 1a: ソース管理にソリューションを追加する  

  - ケース 1b: ソース管理からソリューションを開く  

  - ケース 1c: ソース管理からソリューションを追加する  

- [テスト領域 2: ソース管理から取得](../../extensibility/internals/test-area-2-get-from-source-control.md)  
  
- [テスト領域 3: チェックアウトとチェックアウトの取り消し](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)  
  
  - ケース 3: チェックアウト/チェックアウトの取り消し  

  - ケース 3a: チェックアウト  

  - ケース 3b: 切断されたチェックアウト  

  - ケース 3c: クエリの編集/クエリの保存 (QEQS)  

  - ケース 3d: サイレントチェックアウト  

  - ケース 3e: チェックアウトを元に戻す  
  
- [テスト領域 4: チェックイン](../../extensibility/internals/test-area-4-check-in.md)  
  
  - ケース 4a: 変更された項目  

  - ケース 4b: ファイルの追加  

  - ケース 4c: プロジェクトの追加  
  
- [テスト領域 5: ソース管理の変更](../../extensibility/internals/test-area-5-change-source-control.md)  
  
  - ケース 5a: バインド  

  - ケース 5b: バインド解除  

  - ケース 5c: 再バインド  

- [テスト領域 6: 削除](../../extensibility/internals/test-area-6-delete.md)  

- [テスト領域 7: 共有](../../extensibility/internals/test-area-7-share.md)  

- [テスト領域 8: プラグインの切り替え](../../extensibility/internals/test-area-8-plug-in-switching.md)  

  - ケース 8a: 自動変更  

  - Case 8b: ソリューションベースの変更  

## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
