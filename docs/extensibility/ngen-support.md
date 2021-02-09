---
title: VSIX v3 | での Ngen のサポートMicrosoft Docs
description: ネイティブイメージジェネレーターを有効にする方法について説明します。これは、拡張機能の開発者がマネージアプリケーションのパフォーマンスを向上させるために使用できるツールです。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cc674fbc8930415584eb5bed64f8c9cc67e0a8a2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99886653"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 での Ngen のサポート

Visual Studio 2017 および新しい VSIX v3 (バージョン 3) 拡張機能マニフェスト形式では、拡張機能の開発者はインストール時にアセンブリを "ngen" できるようになりました。

次に示すのは、"ngen" の機能について説明している MSDN の抜粋です。

>ネイティブイメージジェネレーター (*Ngen.exe*) は、マネージアプリケーションのパフォーマンスを向上させるツールです。 *Ngen.exe* は、コンパイルされたプロセッサ固有のマシンコードを含むファイルであるネイティブイメージを作成し、それらをローカルコンピューターのネイティブイメージキャッシュにインストールします。 ランタイムは、Just-In-Time (JIT) コンパイラを使用してオリジナルのアセンブリをコンパイルする代わりに、キャッシュにあるネイティブ イメージを使用できます。
>
>[Ngen.exe から (ネイティブイメージジェネレーター)](/dotnet/framework/tools/ngen-exe-native-image-generator)

アセンブリを "ngen" するには、VSIX を "コンピューターごとにインスタンスごとに" インストールする必要があります。 これを有効にするには、デザイナーで [すべてのユーザー] チェックボックスをオンにし `extension.vsixmanifest` ます。

![すべてのユーザーを確認する](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>Ngen を有効にする方法

アセンブリに対して ngen を有効にするには、Visual Studio の [ **プロパティ** ] ウィンドウを使用します。

次の4つのプロパティを設定できます。

1. **Ngen** (ブール値)-True の場合、Visual Studio インストーラーはアセンブリを "Ngen" します。
2. **Ngen アプリケーション** (string)-ngen は、アセンブリの依存関係を解決するために、アプリケーションの *app.config* ファイルを使用する機会を提供します。 この値は、(Visual Studio のインストールディレクトリを基準として) 使用する *app.config* を持つアプリケーションに設定する必要があります。
3. **Ngen アーキテクチャ** (列挙型)-アセンブリをネイティブにコンパイルするためのアーキテクチャ。 オプションは次のとおりです。 a. NotSpecified が指定されています。 X86 c。 X64 d。 すべて
4. **Ngen の優先度** (1 ~ 3 の整数)-Ngen の優先度レベルは [Ngen.exe の優先度](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)レベルに記載されています。

次に、[ **プロパティ** ] ウィンドウの動作を見てみましょう。

![プロパティでの ngen](media/ngen-in-properties.png)

これにより、VSIX プロジェクトの *.csproj* ファイル内のプロジェクト参照にメタデータが追加されます。

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

プロパティデザイナーの変更は、プロジェクト参照以外にも適用されます。項目が .NET アセンブリである限り、プロジェクト内の項目の Ngen メタデータも設定できます (上記と同じ方法を使用します)。
