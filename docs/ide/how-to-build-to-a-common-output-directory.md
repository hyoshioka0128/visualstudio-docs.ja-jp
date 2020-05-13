---
title: '方法: 共通出力ディレクトリへのビルド'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
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
ms.openlocfilehash: a1e669789d2117b4bd2ee550dfffb147e46620c4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "68416752"
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