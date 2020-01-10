---
title: プロパティ関数 | Microsoft Docs
ms.date: 02/21/2017
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, property functions
ms.assetid: 2253956e-3ae0-4bdc-9d3a-4881dfae4ddb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b0551162a00437b01c7357dfdac16462aad8f2fc
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597387"
---
# <a name="property-functions"></a>プロパティ関数

.NET Framework のバージョン 4 と 4.5 では、プロパティ関数を使用して MSBuild スクリプトを評価できます。 プロパティ関数は、プロパティが表示される場所ならどこでも使用できます。 タスクとは異なり、プロパティ関数はターゲットの外側でも使用でき、ターゲットが実行される前に評価されます。

 MSBuild タスクを使用しなくても、システム時刻の読み取り、文字列の比較、正規表現の照合、その他の処理をビルド スクリプト内で実行できます。 MSBuild は、文字列を数値に、数値を文字列に変換しようと試みます。また、必要に応じて他の変換も実行します。
 
プロパティ関数から返される文字列値は、[特殊文字](msbuild-special-characters.md)がエスケープされます。 プロジェクト ファイルに直接配置した場合と同様に値を扱う場合は、`$([MSBuild]::Unescape())` を使用して特殊文字のエスケープを解除します。

## <a name="property-function-syntax"></a>プロパティ関数の構文

次に 3 種類のプロパティ関数を示します。各関数には異なる構文があります。

- 文字列 (インスタンス) プロパティ関数
- 静的プロパティ関数
- MSBuild プロパティ関数

### <a name="string-property-functions"></a>文字列プロパティ関数

ビルド プロパティの値はすべて文字列値です。 文字列 (インスタンス) メソッドを使用してプロパティ値を操作できます。 たとえば、次のコードを使用して、完全パスを表すビルド プロパティからドライブ名 (最初の 3 文字) を抽出できます。

```fundamental
$(ProjectOutputFolder.Substring(0,3))
```

### <a name="static-property-functions"></a>静的プロパティ関数

ビルド スクリプトで、各種システム クラスの静的プロパティおよびメソッドにアクセスできます。 静的プロパティの値を取得するには、次の構文を使用します。ここで、\<Class> はシステム クラスの名前、\<Property> はプロパティの名前です。

```fundamental
$([Class]::Property)
```

たとえば、次のコードを使用して、ビルド プロパティを現在の日付と時刻に設定します。

```xml
<Today>$([System.DateTime]::Now)</Today>
```

静的メソッドを呼び出すには、次の構文を使用します。ここで、\<Class> はシステム クラスの名前、\<Method> はメソッドの名前、(\<Parameters>) はメソッドのパラメーター リストです。

```fundamental
$([Class]::Method(Parameters))
```

たとえば、ビルド プロパティを新しい GUID に設定するには、次のスクリプトを使用できます。

```xml
<NewGuid>$([System.Guid]::NewGuid())</NewGuid>
```

静的プロパティ関数では、次のシステム クラスの任意の静的メソッドやプロパティを使用できます。

- System.Byte
- System.Char
- System.Convert
- System.DateTime
- System.Decimal
- System.Double
- System.Enum
- System.Guid
- System.Int16
- System.Int32
- System.Int64
- System.IO.Path
- System.Math
- System.Runtime.InteropServices.OSPlatform
- System.Runtime.InteropServices.RuntimeInformation
- System.UInt16
- System.UInt32
- System.UInt64
- System.SByte
- System.Single
- System.String
- System.StringComparer
- System.TimeSpan
- System.Text.RegularExpressions.Regex
- System.UriBuilder
- System.Version
- Microsoft.Build.Utilities.ToolLocationHelper

さらに、次の静的メソッドおよびプロパティを使用できます。

- System.Environment::CommandLine
- System.Environment::ExpandEnvironmentVariables
- System.Environment::GetEnvironmentVariable
- System.Environment::GetEnvironmentVariables
- System.Environment::GetFolderPath
- System.Environment::GetLogicalDrives
- System.IO.Directory::GetDirectories
- System.IO.Directory::GetFiles
- System.IO.Directory::GetLastAccessTime
- System.IO.Directory::GetLastWriteTime
- System.IO.Directory::GetParent
- System.IO.File::Exists
- System.IO.File::GetCreationTime
- System.IO.File::GetAttributes
- System.IO.File::GetLastAccessTime
- System.IO.File::GetLastWriteTime
- System.IO.File::ReadAllText

### <a name="calling-instance-methods-on-static-properties"></a>静的プロパティ上でインスタンス メソッドを呼び出す

オブジェクト インスタンスを返す静的プロパティにアクセスすると、そのオブジェクトのインスタンス メソッドを呼び出すことができます。 インスタンス メソッドを呼び出すには、次の構文を使用します。ここで、\<Class> はシステム クラスの名前、\<Property> はプロパティの名前、\<Method> はメソッドの名前、(\<Parameters>) はメソッドのパラメーター リストです。

```fundamental
$([Class]::Property.Method(Parameters))
```

クラスの名前は、名前空間を使用して完全修飾する必要があります。

たとえば、次のコードを使用して、ビルド プロパティを現在の日付 (今日) に設定します。

```xml
<Today>$([System.DateTime]::Now.ToString('yyyy.MM.dd'))</Today>
```

### <a name="msbuild-property-functions"></a>MSBuild プロパティ関数

ビルド内のいくつかの静的メソッドにアクセスすると、算術、ビットごとの論理、およびエスケープ文字のサポートが提供されます。 次の構文を使用して、これらのメソッドにアクセスします。ここで、\<Method> はメソッドの名前、(\<Parameters>) はメソッドのパラメーター リストです。

```fundamental
$([MSBuild]::Method(Parameters))
```

たとえば、数値を持つ 2 つのプロパティを合計するには、次のコードを使用します。

```fundamental
$([MSBuild]::Add($(NumberOne), $(NumberTwo)))
```

次に MSBuild プロパティ関数の一覧を示します。

|関数シグネチャ|説明|
|------------------------|-----------------|
|double Add(double a, double b)|2 個の倍精度浮動小数点数を加算します。|
|long Add(long a, long b)|2 個の長整数を加算します。|
|double Subtract(double a, double b)|2 個の倍精度浮動小数点数を減算します。|
|long Subtract(long a, long b)|2 個の長整数を減算します。|
|double Multiply(double a, double b)|2 個の倍精度浮動小数点数を乗算します。|
|long Multiply(long a, long b)|2 個の長整数を乗算します。|
|double Divide(double a, double b)|2 個の倍精度浮動小数点数を除算します。|
|long Divide(long a, long b)|2 個の長整数を除算します。|
|double Modulo(double a, double b)|2 個の倍精度浮動小数点数を剰余します。|
|long Modulo(long a, long b)|2 個の長整数を剰余します。|
|string Escape(string unescaped)|MSBuild のエスケープ ルールに従って文字列をエスケープします。|
|string Unescape(string escaped)|MSBuild のエスケープ ルールに従って文字列をエスケープ解除します。|
|int BitwiseOr(int first, int second)|1 番目と 2 番目 (first &#124; second) でビットごとの `OR` を実行します。|
|int BitwiseAnd(int first, int second)|1 番目と 2 番目 (first & second) でビットごとの `AND` を実行します。|
|int BitwiseXor(int first, int second)|1 番目と 2 番目 (first ^ second) でビットごとの `XOR` を実行します。|
|int BitwiseNot(int first)|ビットごとの `NOT` (~first) を実行します。|
|bool IsOsPlatform(string platformString)|現在の OS プラットフォームが `platformString` かどうかを指定します。 `platformString` は <xref:System.Runtime.InteropServices.OSPlatform> のメンバーである必要があります。|
|bool IsOSUnixLike()|現在の OS が Unix システムの場合は true です。|
|string NormalizePath(params string[] path)|指定されたパスの正規化された完全なパスを取得し、現在のオペレーティング システムの適切なディレクトリ区切り文字が含まれていることを確認します。|
|string NormalizeDirectory(params string[] path)|指定されたディレクトリの正規化された完全なパスを取得し、現在のオペレーティング システムの適切なディレクトリ区切り文字が含まれていて、末尾にスラッシュがあることを確認します。|
|string EnsureTrailingSlash(string path)|指定されたパスの末尾にスラッシュがない場合は、追加します。 パスが空の文字列の場合は変更されません。|
|string GetPathOfFileAbove(string file, string startingDirectory)|現在のビルド ファイルの場所に基づいて、または `startingDirectory` に基づいて (指定されている場合)、ファイルを検索します。|
|GetDirectoryNameOfFileAbove(string startingDirectory, string fileName)|指定されたディレクトリまたはそのディレクトリの上のディレクトリ構造内の場所でファイルを見つけます。|
|string MakeRelative(string basePath, string path)|`path` を `basePath` に対して相対的にします。 `basePath` は絶対ディレクトリである必要があります。 `path` を相対にできない場合、verbatim が返されます。 `Uri.MakeRelativeUri` と似ています。|
|string ValueOrDefault(string conditionValue, string defaultValue)|パラメーター 'conditionValue' が空の場合にのみ、パラメーター 'defaultValue' に文字列を返します。それ以外の場合は、値 conditionValue を返します。|

## <a name="nested-property-functions"></a>入れ子になったプロパティ関数

次の例が示すように、プロパティ関数を組み合わせてより複雑な関数を形成します。

```fundamental
$([MSBuild]::BitwiseAnd(32, $([System.IO.File]::GetAttributes(tempFile))))
```

この例では、<xref:System.IO.FileAttributes> というパスにより与えられたファイルの `Archive``tempFile` ビット (32 または 0) の値が返されます。 列挙データ値はプロパティ関数内で名前によって表示できないことに注意してください。 代わりに数値 (32) を使用する必要があります。

入れ子になったプロパティ関数では、メタデータも表示される可能性があります。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。

## <a name="msbuild-doestaskhostexist"></a>MSBuild の DoesTaskHostExist

MSBuild の `DoesTaskHostExist` プロパティ関数は、指定したランタイムとアーキテクチャ値に対してタスク ホストが現在インストールされているかどうかを返します。

このプロパティ関数には次の構文があります。

```fundamental
$([MSBuild]::DoesTaskHostExist(string theRuntime, string theArchitecture))
```

## <a name="msbuild-ensuretrailingslash"></a>MSBuild EnsureTrailingSlash

MSBuild の `EnsureTrailingSlash` プロパティ関数は、末尾のスラッシュがないときにそれを追加します。

このプロパティ関数には次の構文があります。

```fundamental
$([MSBuild]::EnsureTrailingSlash('$(PathProperty)'))
```

## <a name="msbuild-getdirectorynameoffileabove"></a>MSBuild の GetDirectoryNameOfFileAbove

MSBuild の `GetDirectoryNameOfFileAbove` プロパティ関数は、パスの現在のディレクトリの上にあるディレクトリ内でファイルを探します。

 このプロパティ関数には次の構文があります。

```fundamental
$([MSBuild]::GetDirectoryNameOfFileAbove(string ThePath, string TheFile))
```

 次のコードはこの構文の例です。

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))\EnlistmentInfo.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))' != '' " />
```

## <a name="msbuild-getpathoffileabove"></a>MSBuild GetPathOfFileAbove

MSBuild の `GetPathOfFileAbove` プロパティ関数は、直前のファイルのパスを返します。 呼び出しと同じ機能です

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), dir.props))\dir.props" />
```

このプロパティ関数には次の構文があります。

```fundamental
$([MSBuild]::GetPathOfFileAbove(dir.props))
```

## <a name="msbuild-getregistryvalue"></a>MSBuild の GetRegistryValue

MSBuild の `GetRegistryValue` プロパティ関数は、レジストリ キーの値を返します。 この関数は、キー名と値の名前という 2 つの引数を取り、レジストリの値を返します。 値の名前を指定しない場合は、既定値が返されます。

この関数を使用する方法を次の例に示します。

```fundamental
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, ``))                                  // default value
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, `SymbolCacheDir`))
$([MSBuild]::GetRegistryValue(`HKEY_LOCAL_MACHINE\SOFTWARE\(SampleName)`, `(SampleValue)`))             // parens in name and value
```

## <a name="msbuild-getregistryvaluefromview"></a>MSBuild の GetRegistryValueFromView

MSBuild の `GetRegistryValueFromView` プロパティ関数は、レジストリ キー、値、および 1 つ以上の順序づけられたレジストリ ビューを含むシステム レジストリ データを取得します。 キーと値は見つかるまで各レジストリ ビューで順番に検索されます。

このプロパティ関数の構文を次に示します。

```fundamental
[MSBuild]::GetRegistryValueFromView(string keyName, string valueName, object defaultValue, params object[] views)
```

Windows 64 ビット オペレーティング システムは、**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node** というレジストリ キーを保持しています。このキーは、32 ビット アプリケーションに対して **HKEY_LOCAL_MACHINE\SOFTWARE** というレジストリ ビューを提供します。

既定では、WOW64 で実行されている 32 ビット アプリケーションは 32 ビットのレジストリ ビューにアクセスし、64 ビット アプリケーションは 64 ビットのレジストリ ビューにアクセスします。

次のレジストリ ビューが使用できます。

|レジストリ ビュー|定義|
|-------------------|----------------|
|RegistryView.Registry32|32 ビット アプリケーションのレジストリ ビュー。|
|RegistryView.Registry64|64 ビット アプリケーションのレジストリ ビュー。|
|RegistryView.Default|アプリケーションが実行されているプロセスに対応するレジストリ ビュー。|

次に例を示します。

 ```fundamental
$([MSBuild]::GetRegistryValueFromView('HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SDKs\Silverlight\v3.0\ReferenceAssemblies', 'SLRuntimeInstallPath', null, RegistryView.Registry64, RegistryView.Registry32))
```

最初に 64 ビットのレジストリ ビュー、次に 32 ビットのレジストリ ビューを参照して、**ReferenceAssemblies** キーの **SLRuntimeInstallPath** データを取得します。

## <a name="msbuild-makerelative"></a>MSBuild の MakeRelative

MSBuild の `MakeRelative` プロパティ関数は、最初のパスに対する 2 番目のパスの相対パスを返します。 各パスはファイルまたはフォルダです。

このプロパティ関数には次の構文があります。

```fundamental
$([MSBuild]::MakeRelative($(FileOrFolderPath1), $(FileOrFolderPath2)))
```

次のコードはこの構文の例です。

```xml
<PropertyGroup>
    <Path1>c:\users\</Path1>
    <Path2>c:\users\username\</Path2>
</PropertyGroup>

<Target Name = "Go">
    <Message Text ="$([MSBuild]::MakeRelative($(Path1), $(Path2)))" />
    <Message Text ="$([MSBuild]::MakeRelative($(Path2), $(Path1)))" />
</Target>

<!--
Output:
   username\
   ..\
-->
```

## <a name="msbuild-valueordefault"></a>MSBuild の ValueOrDefault

MSBuild の `ValueOrDefault` プロパティ関数は、null または空でない限り、最初の引数を返します。 最初の引数が null または空の場合、関数は 2 番目の引数を返します。

この関数を使用する方法を次の例に示します。

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <Value1>$([MSBuild]::ValueOrDefault('$(UndefinedValue)', 'a'))</Value1>
        <Value2>$([MSBuild]::ValueOrDefault('b', '$(Value1)'))</Value2>
    </PropertyGroup>

    <Target Name="MyTarget">
        <Message Text="Value1 = $(Value1)" />
        <Message Text="Value2 = $(Value2)" />
    </Target>
</Project>

<!--
Output:
  Value1 = a
  Value2 = b
-->
```

## <a name="see-also"></a>関連項目

- [MSBuild プロパティ](../msbuild/msbuild-properties.md)

- [MSBuild の概要](../msbuild/msbuild.md)
