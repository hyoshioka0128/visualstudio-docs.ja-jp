---
title: '方法: 共通出力ディレクトリへのビルド'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- output directory
- builds [Visual Studio], common directory
- common directory
ms.assetid: 1fcc2c48-07cb-4c4f-9556-36945e7dfc4e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a499b5ca5ea64dd9ded10f82b1af43258f346d3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284777"
---
# <a name="how-to-build-to-a-common-output-directory"></a>方法: 共通出力ディレクトリへのビルド

既定では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] は、ソリューションの各プロジェクトを、そのソリューション内の独自のフォルダーにビルドします。 プロジェクトのビルド出力パスを変更して、すべての出力を強制的に同じフォルダーに配置することができます。

## <a name="to-place-all-solution-outputs-in-a-common-directory"></a>すべてのソリューション出力を共通ディレクトリに配置するには

1. ソリューションのいずれかのプロジェクトをクリックします。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

3. プロジェクトの種類に応じて、 **[コンパイル]** タブまたは **[ビルド]** タブのいずれかをクリックし、 **[出力パス]** をそのソリューションのすべてのプロジェクトで使用するフォルダーに設定します。

4. ソリューションのすべてのプロジェクトに対して、手順 1 から 3 を繰り返します。

## <a name="see-also"></a>参照

- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [方法: ビルド出力ディレクトリを変更する](../ide/how-to-change-the-build-output-directory.md)