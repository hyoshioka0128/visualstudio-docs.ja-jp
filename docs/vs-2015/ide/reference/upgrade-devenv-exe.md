---
title: -Upgrade (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /upgrade Devenv switch
- Devenv, /upgrade switch
- upgrade Devenv switch
ms.assetid: 3468045c-5cc9-4157-9a9d-622452145d27
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 24bb6160f9895f129c4d7d36c2b0aa8a56ca282a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657898"
---
# <a name="upgrade-devenvexe"></a>/Upgrade (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソリューション ファイルおよびそのすべてのプロジェクト ファイル、または指定されたプロジェクト ファイルを、そのファイルに対応する現在の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の形式に更新します。

## <a name="syntax"></a>構文

```
devenv SolutionFile | ProjectFile /upgrade
```

## <a name="arguments"></a>引数
 `SolutionFile` ソリューションおよびそのプロジェクト全体をアップグレードする場合は必須です。 ソリューション ファイルのパスと名前です。 ソリューション ファイルの名前のみを入力するか、完全パスと名前を入力できます。 存在しないフォルダー名やファイル名を入力した場合は、フォルダーやファイルが作成されます。

 `ProjectFile` 単一のプロジェクトをアップグレードする場合、必須です。 ソリューション内のプロジェクト ファイルのパスと名前です。 プロジェクト ファイルの名前のみを入力するか、完全パスと名前を入力できます。 存在しないフォルダー名やファイル名を入力した場合は、フォルダーやファイルが作成されます。

## <a name="remarks"></a>解説
 バックアップは自動的に作成され、現在のディレクトリに作成される Backup という名前のディレクトリにコピーされます。

 ソース管理されたソリューションまたはプロジェクトは、アップグレードする前にチェックアウトする必要があります。

 `/upgrade` スイッチを使用した場合、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は起動されません。 アップグレードの結果は、ソリューションまたはプロジェクトの開発言語のアップグレード レポートで参照できます。 エラーや使用方法は返されません。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] でのプロジェクトのアップグレードについて詳しくは、「[How to: Troubleshoot Unsuccessful Visual Studio Project Upgrades (方法: Visual Studio プロジェクトのアップグレードが成功しなかった場合のトラブルシューティング)](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md)」をご覧ください。

## <a name="example"></a>例
 この例では、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ソリューションの既定フォルダーにある "MyProject.sln" という名前のソリューション ファイルをアップグレードします。

```
devenv "MyProject.sln" /upgrade
```

## <a name="see-also"></a>関連項目
 [方法: Visual Studio プロジェクトのアップグレードに失敗した場合のトラブルシューティング](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md) [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)
