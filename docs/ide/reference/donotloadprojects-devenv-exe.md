---
title: -DoNotLoadProjects (devenv.exe)
description: devenv の DoNotLoadProjects コマンド ライン スイッチを使用して、プロジェクトを読み込まずに指定したソリューションを開く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/30/2019
ms.topic: reference
helpviewer_keywords:
- Devenv, /DoNotLoadProjects switch
- /DoNotLoadProjects Devenv switch
- DoNotLoadProjects Devenv switch
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fb43d3a12e50d3f4a7af43721a5e93b769da28ea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907593"
---
# <a name="donotloadprojects-devenvexe"></a>/DoNotLoadProjects (devenv.exe)

**Visual Studio 2019 バージョン 16.1 の新機能**

プロジェクトを読み込むことなく、指定したソリューションを開きます。 詳細については、「[Visual Studio のフィルター処理済みソリューション](../filtered-solutions.md)」をご覧ください。

## <a name="syntax"></a>構文

```shell
devenv /DoNotLoadProjects SolutionName
```

## <a name="arguments"></a>引数

*SolutionName*

必須。 開くソリューションの完全パスと名前。

## <a name="example"></a>例

この例では、プロジェクトを読み込むことなく、ソリューション MySln.sln を開きます。

```shell
devenv /donotloadprojects MySln.sln
```

## <a name="see-also"></a>関連項目

- [Visual Studio のフィルター処理済みソリューション](../filtered-solutions.md)
- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
