---
title: -DoNotLoadProjects (devenv.exe)
ms.date: 04/30/2019
ms.topic: reference
helpviewer_keywords:
- Devenv, /DoNotLoadProjects switch
- /DoNotLoadProjects Devenv switch
- DoNotLoadProjects Devenv switch
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51e3341082ff354fc8bc87a89b3d7bc56e4e7887
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75569856"
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

## <a name="see-also"></a>参照

- [Visual Studio のフィルター処理済みソリューション](../filtered-solutions.md)
- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
