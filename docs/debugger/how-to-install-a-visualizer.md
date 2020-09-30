---
title: ビジュアライザーをインストールする | Microsoft Docs
ms.date: 06/10/2020
ms.topic: how-to
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
ms.openlocfilehash: 6410e9ba1250da5a0a247c786e4aada310186c4a
ms.sourcegitcommit: da7f093db52df5dcd67e0a030e616b307f0dc2a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91211366"
---
# <a name="how-to-install-a-visualizer"></a>方法: ビジュアライザーをインストールする
作成したビジュアライザーは、インストールして初めて [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で使用できるようになります。 ビジュアライザーのインストールは簡単です。

> [!NOTE]
> UWP アプリでは、標準的なテキスト、HTML、XML、および JSON ビジュアライザーがサポートされています。 カスタム (ユーザーが作成した) ビジュアライザーはサポートされていません。

::: moniker range=">=vs-2019"
### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>Visual Studio 2019 用のビジュアライザーをインストールするには

1. 作成したビジュアライザーが含まれる DLL を探します。

   通常は、デバッガー側 DLL とデバッグ対象側 DLL の両方で、ターゲット プラットフォームとして**任意の CPU** が指定されている場合に最適です。 デバッガー側の DLL は、**任意の CPU** または **32 ビット**のいずれかである必要があります。 デバッグ対象側の DLL のターゲット プラットフォームは、デバッグ対象のプロセスに対応している必要があります。

2. [デバッガー側](create-custom-visualizers-of-data.md#to-create-the-debugger-side)の DLL (およびそれが依存するすべての DLL) を、次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath*`\Common7\Packages\Debugger\Visualizers`

    - `My Documents\`*VisualStudioVersion*`\Visualizers`

3. [デバッグ対象側](create-custom-visualizers-of-data.md#to-create-the-visualizer-object-source-for-the-debuggee-side)の DLL を、次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath*`\Common7\Packages\Debugger\Visualizers\`*Framework*

    - `My Documents\`*VisualStudioVersion*`\Visualizers\`*Framework*

    *Framework* は次のいずれかになります。
    - `net2.0`: デバッグ対象で `.NET Framework` ランタイムが実行されている場合。
    - `netstandard2.0`: デバッグ対象で `netstandard 2.0` (`.NET Framework v4.6.1+` または `.NET Core 2.0+`) をサポートするランタイムが使用されている場合。
    - `netcoreapp`: デバッグ対象で `.NET Core` ランタイムが実行されている場合。 (`.NET Core 2.0+` をサポートします)

   スタンドアロン ビジュアライザーを作成する場合は、デバッグ対象側の DLL が必要です。 この DLL には、<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> のメソッドを実装できるデータ オブジェクトのコードが含まれています。

   デバッグ対象側のコードをマルチターゲットにする場合は、サポートされている最小限の TFM のフォルダーにデバッグ対象側の DLL を配置する必要があります。

4. デバッグ セッションを再開します。

> [!NOTE]
> この手順は、Visual Studio 2017 およびそれ以前のバージョンでは異なります。 この記事の[前のバージョン](how-to-install-a-visualizer.md?view=vs-2017&preserve-view=true)をご覧ください。
::: moniker-end

::: moniker range="vs-2017"
### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>Visual Studio 2017 以前用のビジュアライザーをインストールするには

> [!IMPORTANT]
> Visual Studio 2017 およびそれより前のバージョンでは、.NET Framework ビジュアライザーのみがサポートされています。

1. 作成したビジュアライザーを含むダイナミック リンク ライブラリ (DLL: Dynamic Link Library) を探します。

2. DLL を次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath*`\Common7\Packages\Debugger\Visualizers`

    - `My Documents\`*VisualStudioVersion*`\Visualizers`

3. デバッグ セッションを再開します。

> [!NOTE]
> マネージド ビジュアライザーをリモート デバッグで使用するには、DLL をリモート コンピューター上の同じパスにコピーします。
::: moniker-end

## <a name="see-also"></a>関連項目
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)
- [方法: ビジュアライザーを記述する](create-custom-visualizers-of-data.md)
