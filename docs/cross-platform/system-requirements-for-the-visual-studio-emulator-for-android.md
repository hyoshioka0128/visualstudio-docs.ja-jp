---
title: Visual Studio Emulator for Android のシステム要件 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 35e766ad-269f-41e4-ba23-74a556c315f3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee89472ba4773e3b8692b293118bea154504fb55
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916804"
---
# <a name="system-requirements-for-the-visual-studio-emulator-for-android"></a>Visual Studio Emulator for Android のシステム要件

Visual Studio Emulator for Android は、Hyper-V 上で仮想マシンとして動作します。Hyper-V は Windows 8 以降のバージョンの仮想化テクノロジです。 エミュレーターを実行するには、このトピックで説明する Hyper-V の要件をコンピューターが満たしている必要があります。

エミュレーターをインストールすると、その前提条件の構成がセットアップ プログラムで自動的に行われます。 前提条件の構成が正しく設定されると、エミュレーターは正常に動作します。 構成の設定が完了しなかった場合は、必要に応じて前提条件を手動で有効にします。 前提条件を手動で構成する必要がある場合、 [こちら](/previous-versions/windows/apps/jj863509\(v=vs.105\)) で説明されている Windows Phone Emulator と同じ手順とツールを利用してください。

> [!IMPORTANT]
> エミュレーターのセットアップ プログラムでは、Visual Studio Emulator for Android を実行するための前提条件が確認されます。 前提条件が存在しない場合、警告が表示されますが、セットアップでは必要ありません。

## <a name="Checklist"></a> クイック チェックリスト

Visual Studio Emulator for Android を実行するための要件を簡単に確認できるチェックリストです。 詳細については、このトピックの以下のセクションを参照してください。

システム要件

- Hyper-V のサポート (後述の「Hyper-V」の要件を参照してください)

- 6 GB 以上の RAM。

- Windows 8、Windows 8.1、Windows10 以上の Pro エディションの 64 ビット バージョン

- SSSE3 以降をサポートするプロセッサ。

ネットワーク要件

- DHCP

- 自動的に構成された DNS とゲートウェイの設定

Hyper-V の要件

- BIOS で、次の機能がサポートされている必要があります。

  - ハードウェア依存の仮想化

  - 第 2 レベルのアドレス変換 (SLAT)

  - ハードウェア ベースのデータ実行防止 (DEP)

- Windows で、Hyper-V を有効にして実行する必要があります。

- ローカルの Hyper-V Administrators グループのメンバーである必要があります。

## <a name="system-requirements"></a>システム要件
 コンピューターは次の条件を満たしている必要があります。

- Hyper-V のサポート (「 [Hyper-V の要件](#hyper-v-requirements)」を参照してください)

- 6 GB 以上の RAM。

- Windows 8、Windows 8.1、Windows10 以上の Pro エディションの 64 ビット バージョン。

RAM と Windows の要件を確認するには、コントロール パネルで [システムとセキュリティ] を選択し、[システム] を選択します。

![システム必要条件の確認](../cross-platform/media/android_emu_system_requirements.png "Android_Emu_System_Requirements")

## <a name="network-requirements"></a>ネットワーク要件

ネットワークは次の条件を満たしている必要があります。

- DHCP

   エミュレーターは、独自の IP アドレスでネットワーク上に個別のデバイスとして自動的に構成されるため、DHCP が必要です。

- 自動的に構成された DNS とゲートウェイの設定

   エミュレーターの DNS およびゲートウェイ設定を手動で構成することはできません。

  エミュレーターのネットワークの問題を解決する方法については、以下のトピックを参照してください。

- [Troubleshooting the Visual Studio Emulator for Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)

## <a name="hyper-v-requirements"></a>Hyper-V の要件

BIOS での Hyper-V の要件

コンピューターの BIOS は、次の要件をサポートする必要があります。また、次の要件を有効にする必要があります。

- ハードウェア依存の仮想化

- 第 2 レベルのアドレス変換 (SLAT)

- ハードウェア ベースのデータ実行防止 (DEP)

Windows での Hyper-V の要件

コンピューターと BIOS 設定が既に Hyper-V をサポートするよう構成されている場合、セットアップ プログラムで Hyper-V が有効になり、開始されます。 サポートする構成ではない場合は、必要に応じてこれらの要件を手動で有効にします。

|必要条件|この要件を確認して有効にする方法|
|-----------------|----------------------------------------------|
|Hyper-V がインストールされている必要があります。|[Windows Phone エミュレーターの Hyper-V を有効にする](/previous-versions/windows/apps/jj863509(v=vs.105))ために使用する同じ手順に従ってください。<br /><br /> サービス スナップインで **Hyper-V 仮想マシン管理** サービスの状態を確認します。|
|Hyper-V が実行されている必要があります。|サービスの管理の詳細については、以下のトピックを参照してください。<br /><br /> -   [サービスの開始、停止、一時停止、再開、または再起動](https://technet.microsoft.com/library/cc736564\(v=WS.10\).aspx)<br />-   [サービスを開始する方法を構成します。](https://technet.microsoft.com/%20library/cc739213\(v=ws.10\))|

 ローカルの Hyper-V Administrators グループのメンバーである必要があります。

 権限の昇格を確認するメッセージを繰り返し表示せずに Visual Studio Emulator for Android を実行するには、ローカルの Hyper-V Administrators グループのメンバーである必要があります。 SDK をインストールするときに、既にコンピューターのローカル管理者である場合は、SDK のセットアップ プログラムによって Hyper-V Administrators グループに追加されます。 ローカル管理者ではない場合、手動でこの要件を有効にする必要があります。

 エミュレーターを実行した時点で、まだ Hyper-V Administrators グループのメンバーではない場合、グループに参加するように求められます (ダイアログ ボックスは、Windows Phone エミュレーターを参照しています)。 グループに参加するには、管理者権限が必要です。

> [!IMPORTANT]
> グループに参加した場合は、変更を有効にするためにログオフするか、再起動します。

 ![Hyper&#45;V Administrators セキュリティ グループへの参加](../cross-platform/media/android_emu_hyperv_admin.png "Android_Emu_HyperV_Admin")

 手動で自分をグループに追加するには、[ローカル ユーザーとグループ] スナップインを開きます。

## <a name="running-the-emulator-from-a-bootable-vhd-is-not-supported"></a>起動可能な VHD からのエミュレーターの実行はサポートされていません
 起動可能な VHD から Windows を実行しているときに Visual Studio Emulator for Android でアプリを実行しようとすると、一般的にエミュレーターの起動に数分かかるか、起動に失敗します。 エミュレーターの起動に失敗すると、"アプリの配置に失敗しました。 やり直してください。

 この構成はサポートされていません。"と言うメッセージが表示されます。 関連する問題については、「[Visual Studio Emulator for Android のトラブルシューティング](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)」を参照してください。

## <a name="hyper-v-requires-uncompressed-and-unencrypted-files"></a>Hyper-V に必要な圧縮と暗号化が行われていないファイル
 NTFS ファイル システムで構成したハード ドライブで、Hyper-V に使用する仮想ハード ディスク ファイルは、圧縮も暗号化もされていない状態である必要があります。 次のディレクトリが圧縮も暗号化もされていないことを確認してください。

- %localappdata%\Microsoft\XDE

- C:\Program Files (x86)\Microsoft Emulator Manager

- C:\Program Files (x86)\Microsoft Visual Studio Emulator for Android

- %localappdata%\Microsoft\VisualStudioEmulator

ReFS ファイル システムでは、仮想ハード ディスク ファイルの整合性ビットが設定された状態にしておくことはできません。

## <a name="hardware-graphics-forwarding-opengl-es-support-requirements"></a>ハードウェア グラフィックス転送 (OpenGL ES のサポート) の要件

OpenGL ES で使用される GPU など、エミュレーターで GPU の呼び出しをエミュレートするには、適切な DirectX ドライバーがインストールされた DirectX 互換の GPU が必要です。

## <a name="see-also"></a>関連項目

- [Visual Studio Emulator for Android のトラブルシューティング](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)
