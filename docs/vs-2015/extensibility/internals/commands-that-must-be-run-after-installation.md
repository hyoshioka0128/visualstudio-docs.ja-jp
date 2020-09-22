---
title: インストール後に実行する必要があるコマンド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 158119759f8e90161e1f3b5267be498dfc1c9b38
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842141"
---
# <a name="commands-that-must-be-run-after-installation"></a>インストール後に実行する必要があるコマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

.Msi ファイルを使用して拡張機能を展開する場合は、 `devenv /setup` Visual Studio で拡張機能を検出するために、インストールの一部としてを実行する必要があります。  
  
> [!NOTE]
> このトピックの情報は、Visual Studio 2008 以前のバージョンで DevEnv を検索する場合に適用されます。 新しいバージョンの Visual Studio で DevEnv を検出する方法の詳細については、「 [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)」を参照してください。  
  
## <a name="finding-devenvexe"></a>検索 (devenv.exe を)  
 インストーラーによって書き込まれたレジストリ値から各バージョンの devenv.exe を見つけることができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 RegLocator テーブルと AppSearch テーブルを使用して、レジストリ値をプロパティとして格納します。 詳細については、「 [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)」を参照してください。  
  
### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>さまざまなバージョンの Visual Studio から devenv.exe を検索するための RegLocator テーブル行  
  
|Signature_|Root|キー|名前|Type|  
|-----------------|----------|---------|----------|----------|  
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|環境パス|2|  
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|環境パス|2|  
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|環境パス|2|  
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|環境パス|2|  
  
### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>AppSearch 対応する RegLocator テーブル行のテーブル行  
  
|プロパティ|Signature_|  
|--------------|-----------------|  
|DEVENV_EXE_2002|RL_DevenvExe_2002|  
|DEVENV_EXE_2003|RL_DevenvExe_2003|  
|DEVENV_EXE_2005|RL_DevenvExe_2005|  
|DEVENV_EXE_2008|RL_DevenvExe_2008|  
  
 たとえば、Visual Studio インストーラーは **HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\9.0\setup\vs\environmentpath** のレジストリ値を **C:\VS2008\Common7\IDE\devenv.exe**として書き込みます。これはインストーラーが実行する必要のある実行可能ファイルへの完全なパスです。  
  
 **メモ** RegLocator Type 列は2であるため、署名テーブルで追加のバージョン情報を指定する必要はありません。  
  
## <a name="running-devenvexe"></a>devenv.exe の実行  
 AppSearch standard アクションがインストーラーで実行された後、AppSearch テーブル内の各プロパティには、対応するバージョンの Visual Studio の devenv.exe ファイルをポイントする値が含まれます。 指定したレジストリ値が存在しない場合は、そのバージョンの Visual Studio がインストールされていないため、指定したプロパティは null に設定されます。  
  
 Windows インストーラーは、カスタム動作の種類50を通じてプロパティが指す実行可能ファイルの実行をサポートしています。 カスタム動作には、に統合する前に VSPackage が正常にインストールされていることを確認するために、msidbCustomActionTypeInScript (1024) および msidbCustomActionTypeCommit (512) というスクリプト内実行オプションが含まれている必要があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 詳細については、「CustomAction Table」および「Custom Action In-Script Execution Options」を参照してください。  
  
 種類が50のカスタムアクションでは、実行可能ファイルを含むプロパティを、ターゲット列のソース列とコマンドライン引数の値として指定します。  
  
### <a name="customaction-table-rows-to-run-devenvexe"></a>CustomAction を実行するテーブルの行の devenv.exe  
  
|アクション|Type|source|移行先|  
|------------|----------|------------|------------|  
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|  
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|  
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|  
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|  
  
 インストール中に実行するようにスケジュールを設定するには、カスタムアクションを InstallExecuteSequence テーブルに作成する必要があります。 条件列の各行で対応するプロパティを使用して、そのバージョンのがシステムにインストールされていない場合にカスタムアクションが実行されないようにし [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
> [!NOTE]
> `Null` プロパティは、 `False` 条件で使用されるとに評価されます。  
  
 各カスタムアクションのシーケンス列の値は、Windows インストーラーパッケージ内の他のシーケンス値によって異なります。 シーケンス値は、devenv.exe カスタムアクションが InstallFinalize 標準アクションの直前にできるだけ近い場所で実行されるようにする必要があります。  
  
### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>カスタムアクション devenv.exe をスケジュールするための InstallExecuteSequence テーブル  
  
|操作|条件|シーケンス|  
|------------|---------------|--------------|  
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|  
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|  
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|  
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|  
  
## <a name="see-also"></a>参照  
 [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
