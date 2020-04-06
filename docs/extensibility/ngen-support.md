---
title: VSIX v3 での Ngen のサポート |マイクロソフトドキュメント
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cb75b9256ca937106235fa7a7d66d9cec71c9c60
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702397"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 での Ngen のサポート

Visual Studio 2017 および新しい VSIX v3 (バージョン 3) 拡張機能マニフェスト形式を使用すると、拡張機能の開発者はインストール時にアセンブリを "ngen" できます。

以下は、"ngen" の機能を説明する MSDN からの抜粋です。

>ネイティブ イメージ ジェネレーター (*Ngen.exe*) は、マネージ アプリケーションのパフォーマンスを向上させるツールです。 *Ngen.exe は*、コンパイル済みのプロセッサ固有のマシン コードを含むファイルであるネイティブ イメージを作成し、ローカル コンピュータのネイティブ イメージ キャッシュにインストールします。 ランタイムは、Just-In-Time (JIT) コンパイラを使用してオリジナルのアセンブリをコンパイルする代わりに、キャッシュにあるネイティブ イメージを使用できます。
>
>[Ngen.exe から (ネイティブ イメージ ジェネレーター)](/dotnet/framework/tools/ngen-exe-native-image-generator)

アセンブリを "ngen" するには、VSIX を "インスタンスごとコンピューターごと" をインストールする必要があります。 これは、デザイナーで「全ユーザー」チェックボックスをオンにすることで`extension.vsixmanifest`有効にすることができます。

![すべてのユーザーを確認する](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>Ngen を有効にする方法

アセンブリの ngen を有効にするには、Visual Studio の **[プロパティ**] ウィンドウを使用できます。

設定できるプロパティは 4 つあります。

1. **Ngen** (ブール値) - true の場合、Visual Studio インストーラーはアセンブリを "ngen" します。
2. **Ngen アプリケーション**(文字列) - Ngen は、アセンブリの依存関係を解決するために、アプリケーションの*app.config*ファイルを使用する機会を提供します。 この値は、*使用するアプリケーション*に設定する必要があります (Visual Studio インストール ディレクトリに対して相対的)。
3. **Ngen アーキテクチャ**(列挙型) - アセンブリをネイティブにコンパイルするためのアーキテクチャ。 オプションは次のとおりです。 指定されていない b. X86 c. X64 d. すべて
4. **Ngen 優先度**(1 ~ 3 の整数) - Ngen 優先度レベルは[Ngen.exe の優先順位レベル](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)で文書化されています。

[**プロパティ]** ウィンドウの動作を次に示します。

![プロパティの ngen](media/ngen-in-properties.png)

これにより、VSIX プロジェクトの *.csproj*ファイル内のプロジェクト参照にメタデータが追加されます。

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
    <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
    <Name>ClassLibrary1</Name>
    <Ngen>True</Ngen>
    <NgenApplication>vsn.exe</NgenApplication>
    <NgenArchitecture>X86</NgenArchitecture>
    <NgenPriority>2</NgenPriority>
</ProjectReference>
```

> [!NOTE]
> 必要に応じて、.csproj ファイルを直接編集できます。

## <a name="extra-information"></a>追加情報

プロパティ デザイナーの変更は、プロジェクト参照以外にも適用されます。プロジェクト内の項目の Ngen メタデータは、項目が .NET アセンブリである限り、(上記と同じ方法を使用して) 設定できます。
