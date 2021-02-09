---
title: インストール後に実行する必要があるコマンド |Microsoft Docs
description: Visual Studio で .msi ファイルを使用して展開された拡張機能のインストールの一部として実行する必要があるコマンドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: deca5b39701fd073b3191cf7a24d83ccf1e08794
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99884729"
---
# <a name="commands-that-must-be-run-after-installation"></a>インストール後に実行する必要があるコマンド
*.Msi* ファイルを使用して拡張機能を展開する場合は、Visual Studio で拡張機能を検出するために、インストールの一部として **devenv/setup** を実行する必要があります。

> [!NOTE]
> このトピックの情報は、Visual Studio 2008 以前のバージョンで *devenv.exe* を検索する場合に適用されます。 新しいバージョンの Visual Studio で *devenv.exe* を検出する方法の詳細については、「 [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)」を参照してください。

## <a name="find-devenvexe"></a>検索 devenv.exe
 インストーラーによって書き込まれたレジストリ値から各バージョンの *devenv.exe* を見つけることができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 Reglocator テーブルと AppSearch テーブルを使用して、レジストリ値をプロパティとして格納します。 詳細については、「 [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)」を参照してください。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>さまざまなバージョンの Visual Studio から devenv.exe を検索するための RegLocator テーブル行

|署名|Root|キー|名前|Type|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|環境パス|2|
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|環境パス|2|
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|環境パス|2|
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|環境パス|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>AppSearch 対応する RegLocator テーブル行のテーブル行

|プロパティ|署名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 たとえば、Visual Studio インストーラーは、インストーラーが実行する必要のある実行可能ファイルへの完全なパスである **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath** のレジストリ値を *C:\VS2008\Common7\IDE\devenv.exe* として書き込みます。

> [!NOTE]
> RegLocator テーブルの Type 列は2であるため、署名テーブルで追加のバージョン情報を指定する必要はありません。

## <a name="run-devenvexe"></a>実行 devenv.exe
 AppSearch standard アクションがインストーラーで実行された後、AppSearch テーブル内の各プロパティには、対応するバージョンの Visual Studio の *devenv.exe* ファイルをポイントする値が含まれます。 指定したレジストリ値が存在しない場合は、そのバージョンの Visual Studio がインストールされていないため、指定したプロパティは null に設定されます。

 Windows インストーラーは、カスタム動作の種類50を通じてプロパティが指す実行可能ファイルの実行をサポートしています。 カスタムアクションには、VSPackage をに統合する前に `msidbCustomActionTypeInScript` `msidbCustomActionTypeCommit` 正常にインストールされたことを確認するために、スクリプト内実行オプション (1024) と (512) が含まれている必要があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 詳細については、「 [CustomAction table](/windows/desktop/msi/customaction-table) 」および「 [Custom action in-script execution options](/windows/desktop/msi/custom-action-in-script-execution-options)」を参照してください。

 種類が50のカスタムアクションでは、実行可能ファイルを含むプロパティを、ターゲット列のソース列とコマンドライン引数の値として指定します。

### <a name="customaction-table-rows-to-run-devenvexe"></a>CustomAction を実行するテーブルの行の devenv.exe

|アクション|Type|source|移行先|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|

 インストール中に実行するようにスケジュールを設定するには、カスタムアクションを InstallExecuteSequence テーブルに作成する必要があります。 条件列の各行で対応するプロパティを使用して、そのバージョンのがシステムにインストールされていない場合にカスタムアクションが実行されないようにし [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

> [!NOTE]
> Null 値プロパティは、 `False` 条件で使用されるとに評価されます。

 各カスタムアクションのシーケンス列の値は、Windows インストーラーパッケージ内の他のシーケンス値によって異なります。 シーケンス値は、 *devenv.exe* カスタムアクションが installfinalize 標準アクションの直前にできるだけ近い場所で実行されるようにする必要があります。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>カスタムアクション devenv.exe をスケジュールするための InstallExecuteSequence テーブル

|操作|条件|Sequence|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>関連項目
- [Windows インストーラーと共に Vspackage をインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
