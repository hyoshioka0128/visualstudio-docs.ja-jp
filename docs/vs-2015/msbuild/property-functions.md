---
title: プロパティ関数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, property functions
ms.assetid: 2253956e-3ae0-4bdc-9d3a-4881dfae4ddb
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4108e478e9e77a5ed5699b39dfae44884a6befd3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67826170"
---
# <a name="property-functions"></a>プロパティ関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

.NET Framework のバージョン 4 と 4.5 では、プロパティ関数を使用して MSBuild スクリプトを評価できます。 プロパティ関数は、プロパティが表示される場所ならどこでも使用できます。 タスクとは異なり、プロパティ関数はターゲットの外側でも使用でき、ターゲットが実行される前に評価されます。  
  
 MSBuild タスクを使用しなくても、システム時刻の読み取り、文字列の比較、正規表現の照合、その他の処理をビルド スクリプト内で実行できます。 MSBuild は、文字列を数値に、数値を文字列に変換しようと試みます。また、必要に応じて他の変換も実行します。  
  
 **このトピックの内容:**  
  
- [プロパティ関数の構文](#BKMK_Syntax)  
  
  - [文字列プロパティ関数](#BKMK_String)  

  - [静的プロパティ関数](#BKMK_Static)  

  - [静的プロパティでのインスタンスメソッドの呼び出し](#BKMK_InstanceMethods)  

  - [MSBuild プロパティ関数](#BKMK_PropertyFunctions)  
  
- [入れ子になったプロパティ関数](#BKMK_Nested)  
  
- [MSBuild の DoesTaskHostExist](#BKMK_DoesTaskHostExist)  
  
- [MSBuild の GetDirectoryNameOfFileAbove](#BKMK_GetDirectoryNameOfFileAbove)  
  
- [MSBuild の GetRegistryValue](#BKMK_GetRegistryValue)  
  
- [MSBuild の GetRegistryValueFromView](#BKMK_GetRegistryValueFromView)  
  
- [MSBuild の MakeRelative](#BKMK_MakeRelative)  
  
- [MSBuild の ValueOrDefault](#BKMK_ValueOrDefault)  
  
## <a name="property-function-syntax"></a><a name="BKMK_Syntax"></a> プロパティ関数の構文  
 次に 3 種類のプロパティ関数を示します。各関数には異なる構文があります。  
  
- 文字列 (インスタンス) プロパティ関数  
  
- 静的プロパティ関数  
  
- MSBuild プロパティ関数  
  
### <a name="string-property-functions"></a><a name="BKMK_String"></a> 文字列プロパティ関数  
 ビルド プロパティの値はすべて文字列値です。 文字列 (インスタンス) メソッドを使用してプロパティ値を操作できます。 たとえば、次のコードを使用して、完全パスを表すビルド プロパティからドライブ名 (最初の 3 文字) を抽出できます。  
  
 `$(ProjectOutputFolder.Substring(0,3))`  
  
### <a name="static-property-functions"></a><a name="BKMK_Static"></a> 静的プロパティ関数  
 ビルド スクリプトで、各種システム クラスの静的プロパティおよびメソッドにアクセスできます。 静的プロパティの値を取得するには、次の構文を使用します。ここで、 *Class* はシステムクラスの名前、 *property* はプロパティの名前です。  
  
 `$([Class]::Property)`  
  
 たとえば、次のコードを使用して、ビルド プロパティを現在の日付と時刻に設定します。  
  
 `<Today>$([System.DateTime]::Now)</Today>`  
  
 静的メソッドを呼び出すには、次の構文を使用します。ここで、 *Class* はシステムクラスの名前、 *method* はメソッドの名前、 *(Parameters)* はメソッドのパラメーターリストです。  
  
 `$([Class]::Method(Parameters))`  
  
 たとえば、ビルド プロパティを新しい GUID に設定するには、次のスクリプトを使用できます。  
  
 `<NewGuid>$([System.Guid]::NewGuid())</NewGuid>`  
  
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
  
- System.UInt16  
  
- System.UInt32  
  
- System.UInt64  
  
- System.SByte  
  
- System.Single  
  
- System.String  
  
- System.StringComparer  
  
- System.TimeSpan  
  
- System.Text.RegularExpressions.Regex  
  
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
  
### <a name="calling-instance-methods-on-static-properties"></a><a name="BKMK_InstanceMethods"></a> 静的プロパティでのインスタンスメソッドの呼び出し  
 オブジェクト インスタンスを返す静的プロパティにアクセスすると、そのオブジェクトのインスタンス メソッドを呼び出すことができます。 インスタンスメソッドを呼び出すには、次の構文を使用します。ここで、 *Class* はシステムクラスの名前、 *property* はプロパティの名前、 *method* はメソッドの名前、 *(Parameters)* はメソッドのパラメーターリストです。  
  
 `$([Class]::Property.Method(Parameters))`  
  
 クラスの名前は、名前空間を使用して完全修飾する必要があります。  
  
 たとえば、次のコードを使用して、ビルド プロパティを現在の日付 (今日) に設定します。  
  
 `<Today>$([System.DateTime]::Now.ToString("yyyy.MM.dd"))</Today>`  
  
### <a name="msbuild-property-functions"></a><a name="BKMK_PropertyFunctions"></a> MSBuild プロパティ関数  
 ビルド内のいくつかの静的メソッドにアクセスすると、算術、ビットごとの論理、およびエスケープ文字のサポートが提供されます。 これらのメソッドにアクセスするには、次の構文を使用します。ここで、 *method* はメソッドの名前、 *Parameters* はメソッドのパラメーターリストです。  
  
 `$([MSBuild]::Method(Parameters))`  
  
 たとえば、数値を持つ 2 つのプロパティを合計するには、次のコードを使用します。  
  
 `$([MSBuild]::Add($(NumberOne), $(NumberTwo))`  
  
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
  
## <a name="nested-property-functions"></a><a name="BKMK_Nested"></a> 入れ子になったプロパティ関数  
 次の例が示すように、プロパティ関数を組み合わせてより複雑な関数を形成します。  
  
 `$([MSBuild]::BitwiseAnd(32,   $([System.IO.File]::GetAttributes(tempFile))))`  
  
 この例では、<xref:System.IO.FileAttributes> というパスにより与えられたファイルの `Archive``tempFile` ビット (32 または 0) の値が返されます。 列挙データ値はプロパティ関数内で名前によって表示できないことに注意してください。 代わりに数値 (32) を使用する必要があります。  
  
 入れ子になったプロパティ関数では、メタデータも表示される可能性があります。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。  
  
## <a name="msbuild-doestaskhostexist"></a><a name="BKMK_DoesTaskHostExist"></a> MSBuild の doestaskhostexist  
 MSBuild の `DoesTaskHostExist` プロパティ関数は、指定したランタイムとアーキテクチャ値に対してタスク ホストが現在インストールされているかどうかを返します。  
  
 このプロパティ関数には次の構文があります。  
  
```  
$[MSBuild]::DoesTaskHostExist(string theRuntime, string theArchitecture)  
```  
  
## <a name="msbuild-getdirectorynameoffileabove"></a><a name="BKMK_GetDirectoryNameOfFileAbove"></a> MSBuild の GetDirectoryNameOfFileAbove  
 MSBuild の `GetDirectoryNameOfFileAbove` プロパティ関数は、パスの現在のディレクトリの上にあるディレクトリ内でファイルを探します。  
  
 このプロパティ関数には次の構文があります。  
  
```  
$[MSBuild]::GetDirectoryNameOfFileAbove(string ThePath, string TheFile)  
```  
  
 次のコードはこの構文の例です。  
  
```  
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))\EnlistmentInfo.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))' != '' " />  
```  
  
## <a name="msbuild-getregistryvalue"></a><a name="BKMK_GetRegistryValue"></a> MSBuild GetRegistryValue  
 MSBuild の `GetRegistryValue` プロパティ関数は、レジストリ キーの値を返します。 この関数は、キー名と値の名前という 2 つの引数を取り、レジストリの値を返します。 値の名前を指定しない場合は、既定値が返されます。  
  
 この関数を使用する方法を次の例に示します。  
  
```  
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, ``))                                  // default value  
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, `SymbolCacheDir`))  
$([MSBuild]::GetRegistryValue(`HKEY_LOCAL_MACHINE\SOFTWARE\(SampleName)`, `(SampleValue)`))             // parens in name and value  
  
```  
  
## <a name="msbuild-getregistryvaluefromview"></a><a name="BKMK_GetRegistryValueFromView"></a> MSBuild の GetRegistryValueFromView  
 MSBuild の `GetRegistryValueFromView` プロパティ関数は、レジストリ キー、値、および 1 つ以上の順序づけられたレジストリ ビューを含むシステム レジストリ データを取得します。 キーと値は見つかるまで各レジストリ ビューで順番に検索されます。  
  
 このプロパティ関数の構文を次に示します。  
  
 [MSBuild\]::GetRegistryValueFromView(string keyName, string valueName, object defaultValue, params object[] views)  
  
 Windows 64 ビット オペレーティング システムは、HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node というレジストリ キーを保持しています。このキーは、32 ビット アプリケーションに対して HKEY_LOCAL_MACHINE\SOFTWARE というレジストリ ビューを提供します。  
  
 既定では、WOW64 で実行されている 32 ビット アプリケーションは 32 ビットのレジストリ ビューにアクセスし、64 ビット アプリケーションは 64 ビットのレジストリ ビューにアクセスします。  
  
 次のレジストリ ビューが使用できます。  
  
|レジストリ ビュー|定義|  
|-------------------|----------------|  
|RegistryView.Registry32|32 ビット アプリケーションのレジストリ ビュー。|  
|RegistryView.Registry64|64 ビット アプリケーションのレジストリ ビュー。|  
|RegistryView.Default|アプリケーションが実行されているプロセスに対応するレジストリ ビュー。|  
  
 次に例を示します。  
  
 `$([MSBuild]::GetRegistryValueFromView('HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SDKs\Silverlight\v3.0\ReferenceAssemblies', 'SLRuntimeInstallPath', null, RegistryView.Registry64, RegistryView.Registry32))`  
  
 は、最初に 64 ビットのレジストリ ビュー、次に 32 ビットのレジストリ ビューを参照して、ReferenceAssemblies キーの SLRuntimeInstallPath データを取得します。  
  
## <a name="msbuild-makerelative"></a><a name="BKMK_MakeRelative"></a> MSBuild の MakeRelative  
 MSBuild の `MakeRelative` プロパティ関数は、最初のパスに対する 2 番目のパスの相対パスを返します。 各パスはファイルまたはフォルダです。  
  
 このプロパティ関数には次の構文があります。  
  
```  
$[MSBuild]::MakeRelative($(FileOrFolderPath1), $(FileOrFolderPath2))  
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
  
## <a name="msbuild-valueordefault"></a><a name="BKMK_ValueOrDefault"></a> MSBuild の ValueOrDefault  
 MSBuild の `ValueOrDefault` プロパティ関数は、null または空でない限り、最初の引数を返します。 最初の引数が null または空の場合、関数は 2 番目の引数を返します。  
  
 この関数を使用する方法を次の例に示します。  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <Value1>$([MSBuild]::ValueOrDefault(`$(UndefinedValue)`, `a`))</Value1>  
        <Value2>$([MSBuild]::ValueOrDefault(`b`, `$(Value1)`))</Value2>  
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

## <a name="see-also"></a>参照
[MSBuild のプロパティ](msbuild-properties1.md)   
[MSBuild の概要](msbuild.md)
