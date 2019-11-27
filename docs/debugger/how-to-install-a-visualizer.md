---
title: '方法: ビジュアライザーをインストールする |Microsoft Docs'
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
ms.openlocfilehash: 1df72c6978f5ab34a86c74dbc1ea349db5aa4457
ms.sourcegitcommit: b5cb0eb09369677514ee1f44d5d7050d34c7fbc1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491309"
---
# <a name="how-to-install-a-visualizer"></a>方法 : ビジュアライザーをインストールする
作成したビジュアライザーは、インストールして初めて [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で使用できるようになります。 ビジュアライザーのインストールは簡単です。

> [!NOTE]
> UWP アプリでは、標準のテキスト、HTML、XML、および JSON ビジュアライザーのみがサポートされています。 カスタム (ユーザーが作成した) ビジュアライザーはサポートされていません。

### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>ビジュアライザー for Visual Studio 2019 をインストールするには
  
1. 作成したビジュアライザーを含むダイナミック リンク ライブラリ (DLL: Dynamic Link Library) を探します。

2. [デバッガー側](create-custom-visualizers-of-data.md#to-create-the-debugger-side)DLL を次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`
    
3. [デバッグ対象のサイド](create-custom-visualizers-of-data.md#to-create-the-debuggee-side)DLL を次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers\` *Framework*

    - `My Documents\` *VisualStudioVersion* `\Visualizers\` *Framework*

    ここで、 *Framework*は次のいずれかになります。
    - `.NET Framework` ランタイムを実行している debuggees の `net2.0`。
    - `netstandard 2.0` (`.NET Framework v4.6.1+` または `.NET Core 2.0+`) をサポートするランタイムを使用して debuggees を `netstandard2.0` します。
    - `.NET Core` ランタイムを実行している debuggees の `netcoreapp`。 (`.NET Core 2.0+`をサポートします)

4. デバッグ セッションを再開します。

### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>ビジュアライザー for Visual Studio 2017 およびそれ以前のバージョンをインストールするには

> [!IMPORTANT]
> Visual Studio 2017 以前でサポートされているのは .NET Framework ビジュアライザーのみです

1. 作成したビジュアライザーを含むダイナミック リンク ライブラリ (DLL: Dynamic Link Library) を探します。

2. DLL を次のいずれかの場所にコピーします。

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`

3. デバッグ セッションを再開します。

> [!NOTE]
> マネージド ビジュアライザーをリモート デバッグで使用するには、DLL をリモート コンピューター上の同じパスにコピーします。

## <a name="see-also"></a>参照
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)
- [方法 : ビジュアライザーを記述する](create-custom-visualizers-of-data.md)
