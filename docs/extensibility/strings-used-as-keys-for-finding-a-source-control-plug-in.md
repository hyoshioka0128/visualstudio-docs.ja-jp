---
title: ソース管理プラグインを検索するためのキーとして使用される文字列 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, strings used for finding
ms.assetid: c1e31f76-42a1-4c3d-afb2-664044ef12fd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7f9333ff1b6742ca14dc5541bd15e92b2eb39085
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699716"
---
# <a name="strings-used-as-keys-for-finding-a-source-control-plug-in"></a>ソース管理プラグインを検索するためのキーとして使用される文字列
次の文字列は、ソース管理プラグインに関する情報を検索するレジストリにアクセスするためのキーです。

 `STR_SCC_PROVIDER_REG_LOCATION``STR_PROVIDERREGKEY`、、`STR_SCCPROVIDERPATH`および`STR_SCCPROVIDERNAME`は、Dll を Visual Studio のソース管理プラグインとして登録するために使用されるレジストリ キーまたは値です。

 `SCC_PROJECTNAME_KEY`、 `SCC_PROJECTAUX_KEY` `SCC_KEY, SCC_FILE_SIGNATURE`、、`SCC_STATUS_FILE`および MSSCCPRJ の形式を記述するために使用されます。SCC ファイル。

## <a name="string-keys-and-values"></a>文字列キーと値

|Key|値|
|---------|-----------|
|`STR_SCC_PROVIDER_REG_LOCATION`|ソフトウェア\ソースコードコントロールプロバイダ|
|`STR_PROVIDERREGKEY`|プロバイダーの正規表現|
|`STR_SCCPROVIDERPATH`|パス|
|`STR_SCCPROVIDERNAME`|サーバー名|
|`STR_SCC_INI_SECTION`|ソース コード管理|
|`STR_SCC_INI_KEY`|ソース コードコントロール プロバイダー|
|`SCC_PROJECTNAME_KEY`|SCC_Project_Name|
|`SCC_PROJECTAUX_KEY`|SCC_Aux_Path|
|`SCC_STATUS_FILE`|MSSCCPRJ.Scc|
|`SCC_KEY`|SCC|
|`SCC_FILE_SIGNATURE`|ソース コード管理ファイル|
|`SCC_NSE`|名前空間拡張|
|`SCC_NSE_PREFIX`|原語接頭辞|
|`SCC_NSE_DisableOpenSCC`|ソース コントロールを無効にします。|
|`STR_SCCHELPCOLLECTION`|ヘルプコレクション|
|`STR_UI_LANGUAGE`|UILanguage|
|`STR_SRCSAFE_ROOT_KEY`|ソフトウェア\マイクロソフト\ソースセーフ|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [方法: ソース管理プラグインのインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)
