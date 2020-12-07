---
title: -Upgrade (devenv.exe)
description: devenv の Upgrade コマンド ライン スイッチを使用して、ソリューション ファイルとそのすべてのプロジェクト ファイル、または指定したプロジェクト ファイルを、これらのファイルに対する現在の Visual Studio の形式に更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /upgrade Devenv switch
- Devenv, /upgrade switch
- upgrade Devenv switch
ms.assetid: 3468045c-5cc9-4157-9a9d-622452145d27
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2bb0565783efb27cf4194bb25982ee0f717be776
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040954"
---
# <a name="upgrade-devenvexe"></a>/Upgrade (devenv.exe)

ソリューション ファイルおよびそのすべてのプロジェクト ファイル、または指定されたプロジェクト ファイルを、そのファイルに対応する現在の Visual Studio の形式に更新します。

## <a name="syntax"></a>構文

```shell
devenv {SolutionFile|ProjectFile} /Upgrade [/Out OutputFilename]
```

## <a name="arguments"></a>引数

- *SolutionFile*

  ソリューションおよびそのプロジェクト全体をアップグレードする場合は必須です。 ソリューション ファイルのパスと名前です。 ソリューション ファイルの名前のみを入力するか、完全パスと名前を入力できます。 存在しないフォルダー名やファイル名を入力した場合は、フォルダーやファイルが作成されます。

- *ProjectFile*

  単一のプロジェクトをアップグレードする場合、必須です。 ソリューション内のプロジェクト ファイルのパスと名前です。 プロジェクト ファイルの名前のみを入力するか、完全パスと名前を入力できます。 存在しないフォルダー名やファイル名を入力した場合は、フォルダーやファイルが作成されます。

- `/Out` *OutputFilename*

  省略可能。 ツールの出力を送信する先のファイル名。 このファイルが既に存在する場合、ファイルの末尾に出力が追加されます。

## <a name="remarks"></a>注釈

バックアップは自動的に作成され、現在のディレクトリに作成される Backup という名前のディレクトリにコピーされます。

ソース管理されたソリューションまたはプロジェクトは、アップグレードする前にチェックアウトする必要があります。

`/Upgrade` スイッチを使っても、Visual Studio は開きません。 アップグレードの結果は、ソリューションまたはプロジェクトの開発言語のアップグレード レポートで参照できます。 エラーや使用方法は返されません。 Visual Studio でのプロジェクトのアップグレードの詳細については、「[Visual Studio プロジェクトのポート、移行、アップグレード](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)」を参照してください。

## <a name="example"></a>例

この例では、"MyProject.sln" という名前のソリューション ファイルをアップグレードします。

```shell
devenv "%USERPROFILE%\source\repos\MyProject\MyProject.sln" /upgrade
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
