---
title: 以前のバージョンの .NET Framework を F# のターゲットにする
description: Visual Studio で F# を使用するときに、以前のバージョンの .NET Framework をターゲットにする場合について説明します。
ms.date: 07/11/2018
ms.topic: troubleshooting
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
monikerRange: vs-2017
ms.openlocfilehash: 4b5cf62dadc38802e477c7588416b4003304e852
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75584583"
---
# <a name="target-older-versions-of-net-f"></a>以前のバージョンの .NET をターゲットにする (F#)

Visual Studio が Windows 8.1 にインストールされている状態で、F# プロジェクトで .NET Framework 2.0、3.0、または 3.5 をターゲットにしようとすると、次の内容のエラーが表示される場合があります。

**このプロジェクトには 2.0 F# ランタイムが必要ですが、そのランタイムがインストールされていません。**

このエラーは、次の条件の組み合わせで発生することがわかっています。

- Windows 8.1 に Visual Studio をインストールした。

- Visual Studio をインストールする前に、.NET Framework 3.5 を有効にしなかった。

- プロジェクトのターゲットが .NET Framework 2.0、3.0、または 3.5 である。

Visual Studio のインストール時に、インストールされている .NET Framework のバージョンが検出されます。 Visual Studio で F# 2.0 ランタイムがインストールされるのは、.NET Framework 3.5 がインストールされ、有効になっている場合のみです。

## <a name="resolve-the-error"></a>エラーを解決する

このエラーを解決する場合、次のいずれかの操作を行うことができます。

- 新しいバージョンの .NET Framework をターゲットにします。

- Windows 8.1 で .NET Framework 3.5 を有効にしてから、Visual Studio のインストールを修復して F# 2.0 ランタイムをインストールします。 これを行う手順を以下に示します。

### <a name="to-enable-the-net-framework-35-on-windows-81"></a>Windows 8.1 で .NET Framework 3.5 を有効にするには

1. **[スタート]** 画面で、「**コントロール パネル**」と入力します。

   入力すると、 **[アプリ]** 見出しの下に **[コントロール パネル]** アイコンが表示されます。

2. **[コントロール パネル]** アイコン、 **[プログラム]** アイコン、 **[Windows の機能の有効化または無効化]** リンクの順に選択します。

3. **[.NET Framework 3.5 (.NET 2.0 と 3.0 を含む)]** チェック ボックスがオンになっていることを確認してから、 **[OK]** ボタンを選択します。 .NET Framework のオプション コンポーネントに対するすべての子ノードのチェック ボックスをオンにする必要はありません。

   .NET Framework 3.5 が有効になります (まだ有効になっていない場合)。

### <a name="to-install-the-f-20-runtime"></a>F# 2.0 ランタイムをインストールするには

[Visual Studio の修復手順](../install/repair-visual-studio.md)に従ってください。

## <a name="see-also"></a>参照

- [F# ガイド (.NET Framework)](/dotnet/fsharp/)
- [Visual Studio における F#](fsharp-visual-studio.md)
