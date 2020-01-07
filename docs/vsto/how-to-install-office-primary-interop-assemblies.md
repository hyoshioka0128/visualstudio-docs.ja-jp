---
title: '方法: Office プライマリ相互運用機能アセンブリをインストールする方法'
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies [Office development in Visual Studio], installing
- Office primary interop assemblies, installing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ee6755a2d795d2018136785986a5a346ddc07dc6
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551793"
---
# <a name="how-to-install-office-primary-interop-assemblies"></a>方法: Office プライマリ相互運用機能アセンブリをインストールする方法
  Microsoft Office のインストール時に、Office のプライマリ相互運用機能アセンブリ (PIA) をインストールします。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-install-the-pias-when-you-install-office"></a>Office のインストール時に PIA をインストールするには

1. .NET Framework のバージョンが 2.0 以降であることを確認します。

2. Microsoft Office をインストールし、アプリケーションを拡張するための **.NET プログラミング サポート**の機能(この機能は既定のインストールに含まれています)が選択されていることを確認します。

    > [!警告]
    > 既定では、PIA はビルドするときにソリューションに埋め込まれるので、VSTO アドインまたはカスタマイズを使用する前提条件として PIA をユーザーに配布する必要はありません。

## <a name="see-also"></a>関連項目
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [方法: Office ソリューションを開発するコンピューターを構成する方法](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする方法](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Office ソリューションの開発&#40;の概要 VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
