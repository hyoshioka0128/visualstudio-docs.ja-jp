---
title: システム要件の検出 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ab254df5d53f379704128d8860b8d7fe5655bae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708734"
---
# <a name="detect-system-requirements"></a>システム要件の検出
VS パッケージは、Visual Studio がインストールされていない限り機能しません。 VsPackage のインストールを管理するのには、Microsoft Windows インストーラーを使用する場合は、Visual Studio がインストールされているかどうかを検出するインストーラーを構成できます。 また、特定のバージョンの Windows や特定の RAM 容量など、他の要件をシステムで確認するように構成することもできます。

## <a name="detect-visual-studio-editions"></a>ビジュアル スタジオのエディションを検出する
 Visual Studio のエディションがインストールされているかどうかを確認するには、次の表に示すように、**インストール**レジストリ キーの値が適切なフォルダーに *(REG_DWORD) 1*であることを確認します。 Visual Studio エディションの階層があります。

1. エンタープライズ

2. 2 次元形式

3. コミュニティ

新しいエディションをインストールすると、そのエディションのレジストリ キーと以前のエディションのレジストリ キーが追加されます。 つまり、エンタープライズ エディションがインストールされている場合、エンタープライズ版とプロフェッショナル エディションおよびコミュニティ エディションの**インストール**キーは*1*に設定されます。 したがって、必要な最新エディションのみを確認する必要があります。

> [!NOTE]
> 64 ビット バージョンのレジストリ エディタでは、32 ビット キーが**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\**の下に表示されます。 Visual Studio のキーは **、HKEY_LOCAL_MACHINE\ソフトウェア\Wow6432Node\マイクロソフト\DevDiv\vs\サービス\\**の下にあります。

|Product|Key|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\デヴディビジョン\vs\サービス\14.0\エンタープライズ|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\デヴディビジョン\vs\サービス\14.0\プロフェッショナル|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\デヴディビジョン\vs\サービス\14.0\コミュニティ|
|Visual Studio 2015 シェル (統合および分離)|HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\デヴディビジョン\vs\サービス\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>Visual Studio が実行されているタイミングを検出する
 VS パッケージのインストール時に Visual Studio が実行されている場合、VS パッケージを正しく登録できません。 インストーラーは、Visual Studio の実行中を検出し、プログラムのインストールを拒否する必要があります。 Windows インストーラでは、このような検出を有効にするためにテーブル エントリを使用することはできません。 代わりに、次のように、カスタム アクションを作成する必要があります: `EnumProcesses` *devenv.exe*プロセスを検出する関数を使用して、起動条件で使用されるインストーラー プロパティを設定するか、条件付きで Visual Studio を閉じるように求めるダイアログ ボックスを表示します。

## <a name="see-also"></a>関連項目
- [Windows インストーラーを使用して VS パッケージをインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
