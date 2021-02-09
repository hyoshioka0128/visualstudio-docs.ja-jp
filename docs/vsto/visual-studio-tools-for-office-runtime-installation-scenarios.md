---
title: Visual Studio Tools for Office ランタイムのインストールシナリオ
description: Visual Studio 2010 Tools for Office runtime をインストールする方法について説明します。 この記事では、3つのインストールシナリオについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, installation scenarios
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 10b747602a1c5af9f63c567103a80405341019af
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921802"
---
# <a name="visual-studio-tools-for-office-runtime-installation-scenarios"></a>Visual Studio Tools for Office ランタイムのインストールシナリオ
  Visual Studio 2010 Tools for Office runtime は、次の3つの方法でインストールできます。

- Visual Studio のインストール時。

- Microsoft Office のインストール時。

- Visual Studio 2010 Tools for Office runtime 再頒布可能パッケージをインストールするとき。

  インストールされるランタイム コンポーネントは、コンピューターの構成およびインストール シナリオによって異なります。

## <a name="runtime-components-that-are-installed-in-each-installation-scenario"></a>各インストールシナリオでインストールされるランタイムコンポーネント
 Visual Studio 2010 Tools for Office runtime には、Office ソリューションローダー、.NET Framework 3.5 用の Office 拡張機能、以降用の Office 拡張機能の3つのコンポーネントがあります。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ランタイムをインストールすると、常に Office ソリューション ローダーがインストールされます。 .NET Framework 用の Office 拡張機能のインストールは、コンピューターの構成およびインストール シナリオによって異なります。 最初にランタイムをインストールするときにどちらかの Office 拡張機能をインストールできない場合、後で特定の要件を満たすと、インストールされていない Office 拡張機能がランタイムによって自動的にインストールされます。 ランタイムのこの機能は、 *オンデマンドでのインストール* と呼ばれます。

 各ランタイム インストールのシナリオで、既定でインストールされるランタイム コンポーネントを次の表に示します。 各シナリオの詳細については、後で説明します。

|ランタイムのインストール シナリオ|Office ソリューション ローダー|.NET Framework 3.5 用の Office 拡張機能|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] の Office 拡張機能|[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] の Office 拡張機能|
|-----------------------------------|----------------------------|--------------------------------------------------| - |---------------------------------------------------------------------------|
|[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 以降を使用する場合|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|はい|はい|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] あり|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|いいえ|いいえ|
|Office 2010 Service Pack 1 (SP1) 以降を使用する場合|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|○ ([!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] がインストール済みの場合)|いいえ|
|ランタイムの再頒布可能パッケージのインストール時|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|○ ([!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] がインストール済みの場合)|○ ([!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] がインストール済みの場合)|

### <a name="install-the-runtime-with-visual-studio-or-the-microsoft-office-developer-tools-for-visual-studio"></a>Visual Studio または Microsoft Office Developer Tools for Visual Studio を使用してランタイムをインストールする
 Visual Studio の Office Developer Tools をインストールすると、開発用コンピューターに [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] および [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 用の Office 拡張機能が常にインストールされます。 また、.NET Framework 3.5 用の Office 拡張機能は、開発用コンピューターに .NET Framework 3.5 が既に存在している場合にのみインストールされます。 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] をインストールした後で .NET Framework 3.5 をインストールすると、初めて .NET Framework 3.5 を対象とする Office プロジェクトを作成するときに、.NET Framework 3.5 用の Office 拡張機能がランタイムによって自動的にインストールされます。

> [!WARNING]
> [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 以降を使用して .NET Framework 3.5 を対象とする Office プロジェクトを作成することはできません。

 Office developer tools をインストールする方法の詳細については、「 [方法: office ソリューションを開発するようにコンピューターを構成](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)する」を参照してください。

### <a name="install-the-runtime-with-office"></a>Office と共にランタイムをインストールする
 コンピューターに .NET Framework 3.5 が既に存在している場合、Office をインストールすると、.NET Framework 3.5 用の Office 拡張機能がインストールされます。 Office の後で .NET Framework 3.5 をインストールすると、初めて Office アプリケーションが .NET Framework 3.5 を対象とするソリューションを読み込むときに、.NET Framework 3.5 用の Office 拡張機能がランタイムによって自動的にインストールされます。

 Office のインストール時に [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降が既に存在している場合でも、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能は Office と共にインストールされません。

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 用の Office 拡張機能は、Office と共にインストールされます。 エンド ユーザーは、Windows Update をインストールすることで [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 用の Office 拡張機能を取得できます。

 ユーザーがアプリケーションを使用するために必要な拡張機能を持っていることを確認するには、ソリューションの前提条件として、Visual Studio 2010 Tools for Office runtime の再頒布可能パッケージの最新バージョンを追加します。 前提条件の詳細については、「 [Office ソリューションの配置の前提条件](/previous-versions/bb608617(v=vs.110))」を参照してください。

### <a name="install-the-runtime-by-using-the-runtime-redistributable"></a>ランタイムの再頒布可能パッケージを使用してランタイムをインストールする
 ランタイムをインストールするには、Visual Studio 2010 Tools for Office runtime 再頒布可能パッケージを手動で実行するか、Office ソリューションを配置するときに、再頒布可能パッケージを前提条件として追加します。

 Visual Studio 2010 Tools for Office runtime 再頒布可能パッケージを使用してランタイムをインストールすると、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 対応するバージョンの .NET Framework がコンピューターに既に存在する場合は、.NET Framework 3.5 用の office 拡張機能と以降の office 拡張機能がインストールされます。 ランタイムをインストールするときにこれらのバージョンの .NET Framework の 1 つがコンピューターに存在しない場合、その時点では、存在しないバージョンの .NET Framework 用の Office 拡張機能はインストールされません。 存在しないバージョンの .NET Framework を後でインストールすると、次回、対応する Office 拡張機能を必要とするソリューションがインストールされたとき (ClickOnce を使用して配置されたソリューションと共にランタイムがインストールされた場合) または読み込まれたときに (Windows インストーラーを使用して配置されたソリューションと共にランタイムがインストールされた場合)、その拡張機能がランタイムによって自動的にインストールされます。

 ClickOnce ソリューションに必須コンポーネントを含める方法の詳細については、「 [方法: Office ソリューションを実行するためにエンドユーザーのコンピューターに必須コンポーネントをインストールする](/previous-versions/bb608608(v=vs.110))」を参照してください。 再頒布可能パッケージからランタイムを手動でインストールする方法の詳細については、「 [方法: Visual Studio Tools for Office ランタイム再頒布可能](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)パッケージをインストールする」を参照してください。

## <a name="see-also"></a>関連項目
- [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office ランタイムのアセンブリ](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)