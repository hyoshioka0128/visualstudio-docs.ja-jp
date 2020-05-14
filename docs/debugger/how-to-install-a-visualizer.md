---
title: '方法 : ビジュアライザーをインストールする |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers, installing
ms.assetid: 3310ef43-515c-4d97-b0f9-51047247d3da
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 499d644cc8374b070cedaf058b0e4dc17d155bdc
ms.sourcegitcommit: 5d1b2895d3a249c6bea30eb12b0ad7c0f0862d85
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80880261"
---
# <a name="how-to-install-a-visualizer"></a>方法 : ビジュアライザーをインストールする
作成したビジュアライザーは、インストールして初めて [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で使用できるようになります。 ビジュアライザーのインストールは簡単です。

> [!NOTE]
> UWP アプリでは、標準のテキスト、HTML、XML、JSON ビジュアライザーのみがサポートされます。 カスタム (ユーザーが作成した) ビジュアライザーはサポートされていません。

::: moniker range=">=vs-2019"
### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>Visual Studio 2019 のビジュアライザーをインストールするには
  
1. 構築したビジュアライザーを含む DLL を見つけます。

   通常、デバッガー側の DLL とデバッグ対象側の DLL の両方が、ターゲット プラットフォームとして **[Any CPU] を**指定する場合に最適です。 デバッガ側の DLL は **、任意**の CPU または**32 ビット**である必要があります。 デバッグ対象側 DLL のターゲット プラットフォームは、デバッグ対象プロセスに対応する必要があります。

2. [デバッガ側](create-custom-visualizers-of-data.md#to-create-the-debugger-side)DLL (および依存するすべての DLL) を次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`
    
3. [デバッグ対象](create-custom-visualizers-of-data.md#to-create-the-debuggee-side)側 DLL を次のいずれかの場所にコピーします。

    - `\Common7\Packages\Debugger\Visualizers\`*フレームワーク**VisualStudioInstallPath*

    - `My Documents\``\Visualizers\`*フレームワーク**VisualStudioVersion*

    *フレームワーク*は次のいずれかです。
    - `net2.0`ランタイムを実行しているデバッグ対象`.NET Framework`の場合。
    - `netstandard2.0`(または`netstandard 2.0``.NET Framework v4.6.1+``.NET Core 2.0+`) をサポートするランタイムを使用するデバッグ対象の場合。
    - `netcoreapp`ランタイムを実行しているデバッグ対象`.NET Core`の場合。 (サポート`.NET Core 2.0+`)

4. デバッグ セッションを再開します。

> [!NOTE]
> 手順は、Visual Studio 2017 および古いで異なります。 この資料の[前のバージョン](how-to-install-a-visualizer.md?view=vs-2017)を参照してください。
::: moniker-end

::: moniker range="vs-2017"
### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>2017 年以前の Visual Studio ビジュアライザーをインストールするには

> [!IMPORTANT]
> Visual Studio 2017 以前のバージョンでは、.NET フレームワーク ビジュアライザーのみがサポートされます。

1. 作成したビジュアライザーを含むダイナミック リンク ライブラリ (DLL: Dynamic Link Library) を探します。

2. DLL を次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`

3. デバッグ セッションを再開します。

> [!NOTE]
> マネージド ビジュアライザーをリモート デバッグで使用するには、DLL をリモート コンピューター上の同じパスにコピーします。
::: moniker-end

## <a name="see-also"></a>関連項目
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)
- [方法 : ビジュアライザーを記述する](create-custom-visualizers-of-data.md)
