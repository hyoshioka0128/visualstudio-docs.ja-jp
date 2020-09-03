---
title: 列挙子 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65a03a8dc741ec86aca3137f49cd753722ede215
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204563"
---
# <a name="enumerators"></a>列挙子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、ソース管理プラグインが認識する必要があるソース管理プラグイン API の列挙子データ型について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [コマンド コード](../extensibility/command-code-enumerator.md)  
 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)関数と[SccPopulateList](../extensibility/sccpopulatelist-function.md)関数のオプションを列挙します。  
  
 [メッセージ](../extensibility/message-enumerator.md)  
 印刷コールバック、 [Lptextoutproc](../extensibility/lptextoutproc.md)に使用されるフラグを列挙します。  
  
 [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)  
 ソース管理下にあるファイルの状態を指定する名前付き定数値を格納します。  
  
 [ディレクトリの状態コード](../extensibility/directory-status-code-enumerator.md)  
 ソース管理下にあるディレクトリの状態を指定する名前付き定数値を格納します。  
  
## <a name="related-sections"></a>関連項目  
 [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)  
 ソース管理プラグイン SDK を定義し、含まれているリソースについて説明します。  
  
 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)  
 指定されたコマンドの詳細オプションをユーザーに表示します。  
  
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)  
 ファイルの一覧を調べて、現在の状態を確認します。 さらに、は関数を使用して、 `pfnPopulate` ファイルがの条件に一致しない場合に呼び出し元に通知し `nCommand` ます。  
  
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)  
 IDE を介してソース管理プラグインからのメッセージを表示するために [Sccopenproject](../extensibility/sccopenproject-function.md) によって使用されるコールバック関数について説明します。  
  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)  
 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。
