---
title: Emulator for Android のシステム要件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: 35e766ad-269f-41e4-ba23-74a556c315f3
caps.latest.revision: 7
ms.author: crdun
manager: crdun
ms.openlocfilehash: b1b77dc7e01ae791379dda52b305ebcdbbf68447
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841525"
---
# <a name="system-requirements-for-the-visual-studio-emulator-for-android"></a>System requirements for the Visual Studio Emulator for Android
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio Emulator for Android は、Hyper-V 上で仮想マシンとして動作します。Hyper-V は Windows 8 以降のバージョンの仮想化テクノロジです。 エミュレーターを実行するには、このトピックで説明する Hyper-V の要件をコンピューターが満たしている必要があります。

 エミュレーターをインストールすると、その前提条件の構成がセットアップ プログラムで自動的に行われます。 前提条件の構成が正しく設定されると、エミュレーターは正常に動作します。 構成の設定が完了しなかった場合は、必要に応じて前提条件を手動で有効にします。 前提条件を手動で構成する必要がある場合、 [こちら](https://msdn.microsoft.com/library/windows/apps/jj863509\(v=vs.105\).aspx) で説明されている Windows Phone Emulator と同じ手順とツールを利用してください。

> [!IMPORTANT]
> エミュレーターのセットアップ プログラムでは、Visual Studio Emulator for Android を実行するための前提条件が確認されます。 前提条件が存在しない場合、警告が表示されますが、セットアップでは必要ありません。

 このトピックは、次のセクションで構成されています。

- [クイックチェックリスト](#Checklist)

- [システム要件](#System)

- [ネットワークの要件](#Network)

- [Hyper-V の要件](#HyperV)

- [起動可能な VHD からのエミュレーターの実行はサポートされていません](#BootableVHD)

- [Hyper-V に必要な圧縮と暗号化が行われていないファイル](#Files)

## <a name="quick-checklist"></a><a name="Checklist"></a> クイックチェックリスト
 Visual Studio Emulator for Android を実行するための要件を簡単に確認できるチェックリストです。 詳細については、このトピックの以下のセクションを参照してください。

 システム要件

- Hyper-V のサポート (後述の「Hyper-V」の要件を参照してください)

- 6 GB 以上の RAM。

- Windows 8、Windows 8.1、Windows10 以上の Pro エディションの 64 ビット バージョン

- SSSE3 以降をサポートするプロセッサ。

  ネットワークの要件

- [DHCP]

- 自動的に構成された DNS とゲートウェイの設定

  Hyper-V の要件

- BIOS で、次の機能がサポートされている必要があります。

  - ハードウェア補助による仮想化

  - Second Level Address Translation (SLAT)

  - ハードウェアベースのデータ実行防止 (DEP)

- Windows で、Hyper-V を有効にして実行する必要があります。

- ローカルの Hyper-V Administrators グループのメンバーである必要があります。

## <a name="system-requirements"></a><a name="System"></a> システム要件
 コンピューターは次の要件を満たす必要があります。

- Hyper-V のサポート (「 [Hyper-V の要件](#HyperV)」を参照してください)

- 6 GB 以上の RAM。

- Windows 8、Windows 8.1、Windows10 以上の Pro エディションの 64 ビット バージョン。

  RAM と Windows の要件を確認するには、コントロール パネルで [システムとセキュリティ] を選択し、[システム] を選択します。

  ![システム必要条件の確認](../cross-platform/media/android-emu-system-requirements.png "Android_Emu_System_Requirements")

## <a name="network-requirements"></a><a name="Network"></a> ネットワーク要件
 ネットワークは次の条件を満たしている必要があります。

- [DHCP]

   エミュレーターは、独自の IP アドレスでネットワーク上に個別のデバイスとして自動的に構成されるため、DHCP が必要です。

- 自動的に構成された DNS とゲートウェイの設定

   エミュレーターの DNS およびゲートウェイ設定を手動で構成することはできません。

  エミュレーターのネットワークの問題を解決する方法については、以下のトピックを参照してください。

- [Visual Studio Emulator for Android のトラブルシューティング](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)

## <a name="hyper-v-requirements"></a><a name="HyperV"></a> Hyper-v の要件
 BIOS での Hyper-V の要件

 コンピューターの BIOS は、次の要件をサポートする必要があります。また、次の要件を有効にする必要があります。

- ハードウェア補助による仮想化

- Second Level Address Translation (SLAT)

- ハードウェアベースのデータ実行防止 (DEP)

  Windows での Hyper-V の要件

  コンピューターと BIOS 設定が既に Hyper-V をサポートするよう構成されている場合、セットアップ プログラムで Hyper-V が有効になり、開始されます。 サポートする構成ではない場合は、必要に応じてこれらの要件を手動で有効にします。

|必要条件|この要件を確認して有効にする方法|
|-----------------|----------------------------------------------|
|Hyper-V がインストールされている必要があります。|[Windows Phone エミュレーターの Hyper-V を有効にする](https://msdn.microsoft.com/library/windows/apps/jj863509\(v=vs.105\).aspx)ために使用する同じ手順に従ってください。<br /><br /> サービス スナップインで **Hyper-V 仮想マシン管理** サービスの状態を確認します。|
|Hyper-V が実行されている必要があります。|サービスの管理の詳細については、以下のトピックを参照してください。<br /><br /> -   [サービスの開始、停止、一時停止、再開、または再起動](https://technet.microsoft.com/library/cc736564\(v=WS.10\).aspx)<br />-   [サービスの開始方法を構成する](https://technet.microsoft.com/%20library/cc739213\(v=ws.10\))|

 ローカルの Hyper-V Administrators グループのメンバーである必要があります。

 権限の昇格を確認するメッセージを繰り返し表示せずに Visual Studio Emulator for Android を実行するには、ローカルの Hyper-V Administrators グループのメンバーである必要があります。 SDK をインストールするときに、既にコンピューターのローカル管理者である場合は、SDK のセットアップ プログラムによって Hyper-V Administrators グループに追加されます。 ローカル管理者ではない場合、手動でこの要件を有効にする必要があります。

 エミュレーターを実行した時点で、まだ Hyper-V Administrators グループのメンバーではない場合、グループに参加するように求められます (ダイアログ ボックスは、Windows Phone エミュレーターを参照しています)。 グループに参加するには、管理者権限が必要です。

> [!IMPORTANT]
> グループに参加した場合は、変更を有効にするためにログオフするか、再起動します。

 ![Hyper&#45;V Administrators セキュリティ グループへの参加](../cross-platform/media/android-emu-hyperv-admin.png "Android_Emu_HyperV_Admin")

 手動で自分をグループに追加するには、[ローカル ユーザーとグループ] スナップインを開きます。

## <a name="running-the-emulator-from-a-bootable-vhd-is-not-supported"></a><a name="BootableVHD"></a> 起動可能な VHD からのエミュレーターの実行はサポートされていません
 起動可能な VHD から Windows を実行しているときに Visual Studio Emulator for Android でアプリを実行しようとすると、一般的にエミュレーターの起動に数分かかるか、起動に失敗します。 エミュレーターの起動に失敗すると、"アプリの配置に失敗しました。 もう一度やり直してください。

 この構成はサポートされていません。"と言うメッセージが表示されます。 関連する問題については、「 [Troubleshooting the Visual Studio Emulator for Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)」を参照してください。

## <a name="hyper-v-requires-uncompressed-and-unencrypted-files"></a><a name="Files"></a> Hyper-v では圧縮されていないファイルと暗号化されていないファイルが必要
 NTFS ファイル システムで構成したハード ドライブで、Hyper-V に使用する仮想ハード ディスク ファイルは、圧縮も暗号化もされていない状態である必要があります。 次のディレクトリが圧縮も暗号化もされていないことを確認してください。

- %localappdata%\Microsoft\XDE

- C:\Program Files (x86)\Microsoft Emulator Manager

- C:\Program Files (x86)\Microsoft Visual Studio Emulator for Android

- %localappdata%\Microsoft\VisualStudioEmulator

  ReFS ファイル システムでは、仮想ハード ディスク ファイルの整合性ビットが設定された状態にしておくことはできません。

## <a name="hardware-graphics-forwarding-opengl-es-support-requirements"></a>ハードウェア グラフィックス転送 (OpenGL ES のサポート) の要件
 OpenGL ES で使用される GPU など、エミュレーターで GPU の呼び出しをエミュレートするには、適切な DirectX ドライバーがインストールされた DirectX 互換の GPU が必要です。

## <a name="see-also"></a>参照
 [Visual Studio Emulator for Android のトラブルシューティング](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)
