---
title: プロジェクト ファイルとソリューション ファイルの種類 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- File Properties.CopyToOutputDirectory
- File Properties.CustomToolNamespace
- File Properties.FileName
- File Properties.FullPath
- File Properties.BuildAction
- File Properties.CustomTool
- FileProperties
helpviewer_keywords:
- suo files
- file types, Visual Studio
- file extensions
- solutions, solution files
- solution files
- .sln files
- Visual Studio, file types and extensions
- extensions, file types
- sln files
- .suo files
- file extensions, Visual Studio
- file types
ms.assetid: 0ba5007b-465d-4efa-b1e4-f0ee68527649
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 59f9fb1f628da6bc4d958fdca3843adebe61b798
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662145"
---
# <a name="project-and-solution-file-types"></a>プロジェクト ファイルとソリューション ファイルの種類
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、多くの種類のファイルをサポートします。 特定のインストールでは、インストールされるコンポーネントによってサポートされるファイルの種類が決まります。 このトピックでは、いくつかの標準的なインストールでサポートされるソリューション ファイルとプロジェクト ファイルの種類について説明します。 その他のファイルの種類の詳細については、それぞれの種類のファイル名拡張子を使用して検索してください。

## <a name="solution-files-sln-and-suo"></a>ソリューション ファイル (.sln および .suo)
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] では、ソリューション固有の設定を格納するために、2 種類のファイル (.sln および .suo) を使用します。 これらのファイルはまとめてソリューション ファイルと呼ばれており、ソリューション エクスプローラーがファイル管理用のグラフィカル インターフェイスを表示するのに必要な情報が格納されています。 これらのファイルよって、開発タスクに戻るたびに環境を気にする必要はなくなり、プロジェクトと最終的な目標に集中できます。

|拡張子|name|説明|
|---------------|----------|-----------------|
|.sln|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ソリューション|プロジェクト、プロジェクト項目、およびソリューション項目としてまとめます。|
|.suo|ソリューション ユーザー オプション|Visual Studio で行ったブレークポイントなどのユーザー レベルのカスタマイズを追跡します。|

## <a name="project-files"></a>プロジェクト ファイル
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] では、プロジェクト固有の情報を格納するために、さまざまなファイル形式を使用します。 詳細については、次のヘルプ トピックを参照してください。

 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]
 [Visual C++ プロジェクトに対して作成されるファイルの種類](https://msdn.microsoft.com/library/2b0ee2e0-ae81-4185-9bb9-11da3c99a283)

 [Visual C++ プロジェクトの作成と管理](https://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047)

 [Unicode](https://msdn.microsoft.com/library/1002004b-4113-4380-bf63-e1570934b793)

## <a name="see-also"></a>関連項目
 [ソリューションおよびプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)
