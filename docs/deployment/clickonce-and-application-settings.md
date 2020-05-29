---
title: ClickOnce とアプリケーションの設定 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, application settings
ms.assetid: 891caba6-faef-4a3c-8f71-60e6fadb60eb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a72b5bc3f3645d9af1008f2c178ab285e8b45449
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184134"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce とアプリケーション設定
Windows フォームのアプリケーション設定を使用すると、クライアントでカスタムアプリケーションとユーザー設定を簡単に作成、保存、および保守できます。 次のドキュメントでは、ClickOnce アプリケーションでのアプリケーション設定ファイルの動作と、ユーザーが次のバージョンにアップグレードしたときに ClickOnce が設定を移行する方法について説明します。

 以下の情報は、既定のアプリケーション設定プロバイダーであるクラスにのみ適用され <xref:System.Configuration.LocalFileSettingsProvider> ます。 カスタムプロバイダーを提供する場合、そのプロバイダーは、データの格納方法と、バージョン間での設定のアップグレード方法を決定します。 アプリケーション設定プロバイダーの詳細については、「[アプリケーション設定のアーキテクチャ](/dotnet/framework/winforms/advanced/application-settings-architecture)」を参照してください。

## <a name="application-settings-files"></a>アプリケーション設定ファイル
 アプリケーション設定は、 * \<app> .exe .config*と*user .config*の2つのファイルを使用します。ここで、 *app*は Windows フォームアプリケーションの名前です。 ユーザーは、アプリケーションでユーザースコープ設定を初めて保存するときに、クライアントに対して作成され*ます。* これに対して、設定の既定値を定義すると、配置前に* \<app> .exe*が存在します。 このファイルは、 **Publish**コマンドを使用すると、Visual Studio によって自動的にインクルードされます。 *Mage.exe*または*mageui.exe*を使用して ClickOnce アプリケーションを作成する場合は、アプリケーションマニフェストにデータを設定するときに、このファイルがアプリケーションの他のファイルに含まれていることを確認する必要があります。

 ClickOnce を使用して配置されていない Windows フォームアプリケーションでは、アプリケーションの* \<app> .exe .config*ファイルはアプリケーションディレクトリに格納され、*ユーザーの .config*ファイルはユーザーの**Documents and Settings**フォルダーに格納されます。 ClickOnce アプリケーションでは、 * \<app> .exe .Config*は clickonce アプリケーションキャッシュ内のアプリケーションディレクトリに存在し、*ユーザー .config*はそのアプリケーションの clickonce データディレクトリに存在します。

 アプリケーションをどのように配置するかに関係なく、アプリケーション設定により、app.config に安全に読み取りアクセスできるようになります。また、 *app.config*への安全な読み取り/書き込み* \<app> アクセスが保証*されます。

 ClickOnce アプリケーションでは、アプリケーション設定で使用される構成ファイルのサイズは、ClickOnce キャッシュのサイズによって制限されます。 詳細については、「 [ClickOnce キャッシュの概要](../deployment/clickonce-cache-overview.md)」を参照してください。

## <a name="version-upgrades"></a>バージョンのアップグレード
 ClickOnce アプリケーションの各バージョンが他のすべてのバージョンから分離されているのと同様に、ClickOnce アプリケーションのアプリケーション設定は、他のバージョンの設定からも分離されます。 ユーザーがアプリケーションの新しいバージョンにアップグレードすると、アプリケーションの設定によって、最新の (最も番号が付いた) バージョンの設定が更新されたバージョンで提供される設定と比較され、設定が新しい設定ファイルセットにマージされます。

 次の表は、どの設定をコピーするかをアプリケーション設定が決定する方法を示しています。

|変更の種類|アップグレード アクション|
|--------------------|--------------------|
|設定が* \<app> .exe. .config*に追加されました|新しい設定は、現在のバージョンの* \<app> .exe. .config*にマージされます。|
|設定が* \<app> .exe. .config*から削除されました|以前の設定は、現在のバージョンの* \<app> .exe. .config*から削除されます。|
|設定の既定値が変更されました。*ユーザー .config*でローカル設定が元の既定値に設定されたままになる|設定は現在のバージョンの app.config にマージされ、新しい既定値が値として使用され*ます。*|
|設定の既定値が変更されました。ユーザー .config で既定以外の設定に設定さ*れています*|設定は、既定値以外の値が保持されている現在のバージョンのユーザー .config にマージされ*ます。*|

独自のアプリケーション設定ラッパークラスを作成し、更新ロジックをカスタマイズしたい場合は、メソッドをオーバーライドでき <xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A> ます。

## <a name="clickonce-and-roaming-settings"></a>ClickOnce とローミングの設定
 ClickOnce はローミング設定では機能しないため、設定ファイルはネットワーク上の複数のコンピューターにわたってフォローできます。 ローミング設定が必要な場合は、ネットワーク経由で設定を保存するアプリケーション設定プロバイダーを実装するか、リモートコンピューターに設定を格納するための独自のカスタム設定クラスを作成する必要があります。 設定プロバイダーの詳細については、「[アプリケーション設定のアーキテクチャ](/dotnet/framework/winforms/advanced/application-settings-architecture)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [アプリケーション設定の概要](/dotnet/framework/winforms/advanced/application-settings-overview)
- [ClickOnce キャッシュの概要](../deployment/clickonce-cache-overview.md)
- [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)