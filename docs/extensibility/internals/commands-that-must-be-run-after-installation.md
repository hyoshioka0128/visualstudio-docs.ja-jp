---
title: インストール後に実行する必要があるコマンド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 77add5afd5d44358f0077a11bb70559a796e74c6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709473"
---
# <a name="commands-that-must-be-run-after-installation"></a>インストール後に実行する必要があるコマンド
*.msi*ファイルを使用して拡張機能を配置する場合は、Visual Studio が拡張機能を検出するために、インストールの一部として**devenv /setup**を実行する必要があります。

> [!NOTE]
> このトピックの情報は、Visual Studio 2008 以前の*devenv.exe*を検索する場合に適用されます。 新しいバージョンの Visual Studio で*devenv.exe*を検出する方法については、「[システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)」を参照してください。

## <a name="find-devenvexe"></a>devenv.exe を探します。
 各バージョンの*devenv.exe*は、RegLocator テーブル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]と AppSearch テーブルを使用してレジストリ値をプロパティとして格納し、インストーラーが書き込むレジストリ値から検索できます。 詳細については、[システム要件の検出を](../../extensibility/internals/detecting-system-requirements.md)参照してください。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>異なるバージョンの Visual Studio から devenv.exe を検索する RegLocator テーブルの行

|署名|Root|Key|名前|種類|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|ソフトウェア\マイクロソフト\ビジュアルスタジオ\7.0\セットアップ\VS|環境パス|2|
|RL_DevenvExe_2003|2|ソフトウェア\マイクロソフト\ビジュアルスタジオ\7.1\セットアップ\VS|環境パス|2|
|RL_DevenvExe_2005|2|ソフトウェア\マイクロソフト\ビジュアルスタジオ\8.0\セットアップ\VS|環境パス|2|
|RL_DevenvExe_2008|2|ソフトウェア\マイクロソフト\ビジュアルスタジオ\9.0\セットアップ\VS|環境パス|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>対応する RegLocator テーブル行の AppSearch テーブル行

|プロパティ|署名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 たとえば、Visual Studio インストーラーは **、HKEY_LOCAL_MACHINE\ソフトウェア\VisualStudio\9.0\セットアップ\VS\環境パス**のレジストリ値を*C:\VS2008\Common7\IDE\devenv.exe*として書き込みます。

> [!NOTE]
> RegLocator テーブルの [型] 列は 2 であるため、追加のバージョン情報を [署名] テーブルで指定する必要はありません。

## <a name="run-devenvexe"></a>devenv.exe を実行します。
 インストーラーで AppSearch の標準アクションを実行した後、AppSearch テーブルの各プロパティには、対応するバージョンの Visual Studio の*devenv.exe*ファイルを示す値が含まれます。 指定されたレジストリ値のいずれかが存在しない場合 (Visual Studio のバージョンがインストールされていないため)、指定されたプロパティは null に設定されます。

 Windows インストーラは、カスタム 動作の種類 50 を通じてプロパティが指す実行可能ファイルの実行をサポートします。 カスタム アクションには、VSPackage がに統合する`msidbCustomActionTypeInScript`前に正常にインストールされていることを確認`msidbCustomActionTypeCommit`するために、スクリプト内実行オプション (1024) と (512)[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を含める必要があります。 詳細については、「 [CustomAction テーブル](/windows/desktop/msi/customaction-table)」および「[カスタム アクションスクリプト内実行オプション](/windows/desktop/msi/custom-action-in-script-execution-options)」を参照してください。

 50 型のカスタム アクションでは、実行可能ファイルを含むプロパティをソース列の値として指定し、Target 列のコマンド ライン引数を指定します。

### <a name="customaction-table-rows-to-run-devenvexe"></a>devenv.exe を実行するカスタムアクション テーブル行

|アクション|Type|source|移行先|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/セットアップ|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/セットアップ|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/セットアップ|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/セットアップ|

 カスタム アクションをインストール中に実行するようにスケジュールするには、カスタム アクションを InstallExecuteSequence テーブルに作成する必要があります。 のバージョンがシステムにインストールされていない場合にカスタム アクションが実行されないようにするには、Condition 列の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]各行の対応するプロパティを使用します。

> [!NOTE]
> Null 値のプロパティは、`False`条件で使用された場合に評価されます。

 カスタム動作ごとの [シーケンス] 列の値は、Windows インストーラ パッケージの他のシーケンス値によって異なります。 シーケンス値は、InstallFinalize 標準アクションの直前に *、devenv.exe*カスタム動作ができるだけ近くで実行されるようにする必要があります。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>カスタム動作をスケジュールするためのテーブルの実行

|アクション|条件|Sequence|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>関連項目
- [Windows インストーラーを使用して VS パッケージをインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
