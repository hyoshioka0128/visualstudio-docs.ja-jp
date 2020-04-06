---
title: IDE によって実装されるコールバック関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 666486f5b800707a4467a129abeed7a13306f10a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739895"
---
# <a name="callback-functions-implemented-by-the-ide"></a>IDE によって実装されるコールバック関数
統合開発環境 (IDE) との統合を可能な限りシームレスにし、統一されたエンドユーザー エクスペリエンスを提供するために、ソース管理プラグインは IDE によって実装されるコールバック関数を使用できます。 プラグインは、ソース管理操作中に適切な時間にこれらの関数を呼び出して、IDE に情報を渡すことができます。IDE は、この情報をネイティブ UI に埋め込み要素として表示できます。 このシナリオでは、プラグインが独自の UI を採用した場合よりも、ユーザーの断片化が少なくなります。

 必要なヘッダー ファイルは*scc.h*です。 既定の場所は*\プログラム ファイル\VSIP 8.0\EnvSDK\common\inc\\です*。 また、ソース管理プラグインのサンプルが*\Program Files\VSIP 8.0\MSSCCI\\*にある VSIP フォルダ内にもあります。

## <a name="in-this-section"></a>このセクションの内容
- [を実行します。](../extensibility/lptextoutproc.md)ソース管理プラグインからのメッセージを IDE で表示するために[SccOpenProject](../extensibility/sccopenproject-function.md)によって使用されるコールバック関数について説明します。

- [ポップリストファンク](../extensibility/poplistfunc.md)バージョン管理下にあるファイルの完全な一覧など、ソース管理プラグインでのみ使用可能な情報に対して IDE が完全にアクセスできない場合に[、SccPopulateList](../extensibility/sccpopulatelist-function.md)によって使用されるコールバック関数について説明します。

- [クエリチェンジFUNC](../extensibility/querychangesfunc.md)[SccQueryChanges](../extensibility/sccquerychanges-function.md)操作で使用されるコールバック関数について説明します。

- [ポプディリストファンク](../extensibility/popdirlistfunc.md)操作で使用されるコールバック関数[について説明します](../extensibility/sccpopulatedirlist-function.md)。

- [オプトネームチェンジプン](../extensibility/optnamechangepfn.md)ソース管理プラグインが名前の変更を IDE に反映できるようにする[SccSetOption](../extensibility/sccsetoption-function.md)の呼び出しによって設定されるコールバック関数について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトを開く](../extensibility/sccopenproject-function.md)プロジェクトを開きます。

- [一覧](../extensibility/sccpopulatelist-function.md)ファイルのリストで現在のステータスを調べます。 また、ファイルが`pfnPopulate`の条件に一致しない場合に、この関数を使用して呼`nCommand`び出し元に通知します。

- [リスト](../extensibility/sccpopulatedirlist-function.md)ソース管理下にあるプロジェクト内のディレクトリとファイルの一覧を調べます。 見つかった各ディレクトリとファイル名は、コールバック関数に渡されます。

- [SccQuery 変更](../extensibility/sccquerychanges-function.md)ファイルの一覧に対して行われた名前の変更を調べます。 各ファイル名は、変更ステータスとともにコールバック関数に渡されます。

- [オプション](../extensibility/sccsetoption-function.md)さまざまなオプションを設定します。 各オプションは、`SCC_OPT_xxx`最初に、独自に定義された値のセットを持ちます。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)ソース管理プラグイン SDK の参照セクションの内容について説明します。
