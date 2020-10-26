---
title: IDE によって実装されるコールバック関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: df2daef11303e85d5fe2d0bf33e3df038081db64
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184529"
---
# <a name="callback-functions-implemented-by-the-ide"></a>IDE で実装されるコールバック関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

統合開発環境 (IDE: integrated development environment) との統合を可能な限りシームレスに行うために、統合されたエンドユーザーエクスペリエンスを提供するために、ソース管理プラグインは、IDE によって実装されるコールバック関数を使用できます。 プラグインは、ソース管理操作中に適切なタイミングでこれらの関数を呼び出して、IDE に情報を渡すことができます。IDE では、この情報をネイティブ UI の埋め込み要素として表示できます。 このシナリオでは、プラグインが独自の UI を使用した場合よりも、ユーザーの断片化が少なくなります。  
  
 必要なヘッダーファイルは scc です。 既定の場所は、Files\VSIP 8.0 \ EnvSDK\common\inc \\ です。 また、ソース管理プラグインのサンプルが MSSCCI にある VSIP フォルダーにもあり \\ ます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)  
 IDE を介してソース管理プラグインからのメッセージを表示するために [Sccopenproject](../extensibility/sccopenproject-function.md) によって使用されるコールバック関数について説明します。  
  
 [POPLISTFUNC](../extensibility/poplistfunc.md)  
 バージョン管理されているファイルの完全な一覧など、ソース管理プラグインでのみ使用できる情報に IDE が完全にアクセスできない場合に、 [SccPopulateList](../extensibility/sccpopulatelist-function.md) によって使用されるコールバック関数について説明します。  
  
 [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)  
 [Sccquerychanges](../extensibility/sccquerychanges-function.md)操作で使用されるコールバック関数について説明します。  
  
 [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)  
 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)操作で使用されるコールバック関数について説明します。  
  
 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)  
 ソース管理プラグインが名前の変更を IDE に戻すことができるようにする [Sccsetoption](../extensibility/sccsetoption-function.md) の呼び出しによって設定されるコールバック関数について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [SccOpenProject](../extensibility/sccopenproject-function.md)  
 プロジェクトを開きます。  
  
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)  
 ファイルの一覧を調べて、現在の状態を確認します。 さらに、は関数を使用して、 `pfnPopulate` ファイルがの条件に一致しない場合に呼び出し元に通知し `nCommand` ます。  
  
 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)  
 ソース管理下にあるプロジェクトまたはプロジェクト内のディレクトリとファイルの一覧を調べます。 見つかった各ディレクトリとファイル名は、コールバック関数に渡されます。  
  
 [SccQueryChanges](../extensibility/sccquerychanges-function.md)  
 ファイルの一覧に対して行われた名前の変更を調べます。 各ファイル名は、コールバック関数に変更状態と共に渡されます。  
  
 [SccSetOption](../extensibility/sccsetoption-function.md)  
 さまざまなオプションを設定します。 各オプションはで始まり `SCC_OPT_xxx` 、独自に定義された値のセットを持ちます。  
  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)  
 ソース管理プラグイン SDK の参照セクションの内容について説明します。
