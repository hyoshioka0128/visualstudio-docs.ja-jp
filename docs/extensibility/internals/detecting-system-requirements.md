---
title: システム要件の検出 |Microsoft Docs
description: Microsoft Windows インストーラーを構成して、インストールされている Visual Studio のエディションなどのシステム要件を検出する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb00ca42376f8b7c150552c862bba7a24a5c1fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056767"
---
# <a name="detect-system-requirements"></a>システム要件の検出
VSPackage は、Visual Studio がインストールされていない場合は機能しません。 Microsoft Windows インストーラーを使用して VSPackage のインストールを管理する場合、Visual Studio がインストールされているかどうかを検出するようにインストーラーを構成できます。 また、特定のバージョンの Windows や特定の RAM 容量など、システムに他の要件がないかどうかを確認するように構成することもできます。

## <a name="detect-visual-studio-editions"></a>Visual Studio のエディションの検出
 Visual Studio のエディションがインストールされているかどうかを確認するには、次の表に示すように、 **インストール** レジストリキーの値が適切なフォルダーの *(REG_DWORD) 1* であることを確認します。 Visual Studio の各エディションの階層があることに注意してください。

1. エンタープライズ

2. 2 次元形式

3. コミュニティ

新しいエディションがインストールされると、そのエディションのレジストリキーだけでなく、以前のエディションにも追加されます。 つまり、Enterprise edition がインストールされている場合は、Enterprise、Professional、Community の各エディションの **インストール** キーが *1* に設定されます。 そのため、必要な最新のエディションのみを確認する必要があります。

> [!NOTE]
> 64ビット版のレジストリエディターでは、32ビットのキーが [ **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\**] の下に表示されます。 Visual Studio のキーが **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\\** になっています。

|製品|キー|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|
|Visual Studio 2015 シェル (統合および分離)|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>Visual Studio が実行されていることを検出する
 VSPackage がインストールされているときに Visual Studio が実行されている場合は、VSPackage を正しく登録できません。 インストーラーは、Visual Studio が実行されていることを検出してから、プログラムのインストールを拒否する必要があります。 Windows インストーラーでは、このような検出を有効にするためにテーブルエントリを使用することはできません。 代わりに、次のように、カスタムアクションを作成する必要があります。関数を使用して `EnumProcesses` *devenv.exe* プロセスを検出し、起動条件で使用されるインストーラープロパティを設定するか、Visual Studio を閉じるようユーザーに求めるダイアログボックスを条件付きで表示します。

## <a name="see-also"></a>こちらもご覧ください
- [Windows インストーラーと共に Vspackage をインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
