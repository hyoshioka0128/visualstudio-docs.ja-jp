---
title: Web.Config ファイル - 動的 ASP.NET アプリのインストルメント化とプロファイリング
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a92e5692-2183-4ae3-9431-b067c6a7aab4
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 9682fe820e34e8e30a3c57670f5e5fbc7eae2153
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809597"
---
# <a name="how-to-modify-webconfig-files-to-instrument-and-profile-dynamically-compiled-aspnet-web-applications"></a>方法: Web.config ファイルを変更して、動的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化およびプロファイルする
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのインストルメンテーション方式を使用すると、動的にコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションから、詳しいタイミング データ、.NET のメモリの割り当てデータ、.NET オブジェクトの有効期間に関するデータを収集できます。

 このトピックでは、*web.config* 構成ファイルを変更して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションのインストルメント化とプロファイルを有効にする方法について説明します。

> [!NOTE]
> サンプリング プロファイル方式を使用する場合や、プリコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] モジュールをインストルメント化する場合は、*web.config* ファイルを変更する必要はありません。

 *web.config* ファイルのルートは、**configuration** 要素です。 動的にコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションをインストルメント化およびプロファイルするには、次の要素を追加するか変更する必要があります。

- プロファイリングを制御する Microsoft.VisualStudio.Enterprise.ASPNetHelper アセンブリを識別する **configuration/runtime/assemblyBinding/dependentAssembly** 要素。 **dependentAssembly** 要素には、2 つの子要素、**assemblyIdentity** と **codeBase** が含まれます。

- ターゲット アセンブリに対するプロファイラーの処理後のコンパイル手順を指定する **configuration/system.web/compilation** 要素。

- プロファイリング ツールの場所を識別する 2 つの **add** 要素が **configuration/appSettings** セクションに追加されます。

  アプリケーションの構成を復元するために使用できるように、変更前の *web.config* ファイルのコピーを作成することをお勧めします。

### <a name="to-add-the-aspnethelper-assembly-as-a-configurationruntimeassemblybindingdependentassembly-element"></a>ASPNetHelper アセンブリを configuration/runtime/assemblyBinding/dependentAssembly 要素として追加するには

1. 必要に応じて、**configuration** 要素の子要素として **runtime** 要素を追加します。追加しない場合は次の手順に進みます。

    **runtime** 要素には、属性はありません。 **configuration** 要素には、**runtime** 子要素を 1 つだけ含めることができます。

2. 必要に応じて、**runtime** 要素の子要素として **assemblyBinding** 要素を追加します。追加しない場合は次の手順に進みます。

    **runtime** 要素には、**assemblyBinding** 要素を 1 つだけ含めることができます。

3. **assemblyBinding** 要素に、次の属性名と値を追加します。

   | 属性名 | 属性の値 |
   |----------------|--------------------------------------|
   | **Xmlns** | **urn:schemas-microsoft-com:asm.v1** |

4. **assemblyBinding** 要素の子要素として **dependentAssembly** 要素を追加します。

    **dependentAssembly** 要素には属性がありません。

5. **dependentAssembly** 要素の子として **assemblyIdentity** 要素を追加します。

6. **assemblyIdentity** 要素に、次の属性名と値を追加します。

   | 属性名 | 属性の値 |
   |--------------------| - |
   | **name** | **Microsoft.VisualStudio.Enterprise.ASPNetHelper** |
   | **PublicKeyToken** | **b03f5f7f11d50a3a** |
   | **culture** | **Neutral** |

7. **dependentAssembly** 要素の子として **codeBase** 要素を追加します。

8. **codeBase** 要素に、次の属性名と値を追加します。

   |属性名|属性の値|
   |--------------------|---------------------|
   |**version**|**10.0.0.0**|
   |**href**|`PathToASPNetHelperDll`|

    `PathToASPNetHelperDll` は、Microsoft.VisualStudio.Enterprise.ASPNetHelper.dll のファイル URL です。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] が既定の場所にインストールされている場合、**href** 値は `C:/Program%20Files/Microsoft%20Visual%20Studio%202010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL` となります。

```xml
    <configuration>
        <runtime>
            <assemblyBinding
                xmlns="urn:schemas-microsoft-com:asm.v1"
            >
                <dependentAssembly>
                    <assemblyIdentity name="Microsoft.VisualStudio.Enterprise.ASPNetHelper"
                        publicKeyToken="b03f5f7f11d50a3a"
                        culture="neutral"
                    />
                    <codeBase
                        version="10.0.0.0"
                        href="file:///C:/Program%20Files/Microsoft%20Visual%20Studio%2010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL"
                    />
                </dependentAssembly>
            </assemblyBinding>
        </runtime>
```

### <a name="to-add-the-profiler-post-process-step-to-the-configurationsystemwebcompilation-element"></a>configuration/system.web/compilation 要素にプロファイラーの処理後の手順を追加するには

1. 必要に応じて、**configuration** 要素の子要素として **system.web** 要素を追加します。追加しない場合は次の手順に進みます。

     **system.web** 要素には属性はありません。 **configuration** 要素には、**system.web** 子要素を 1 つだけ含めることができます。

2. 必要に応じて、**system.web** 要素の子要素として **compilation** 要素を追加します。追加しない場合は次の手順に進みます。

     **system.web** 要素には、**compilation** 子要素を 1 つだけ含めることができます。

3. **compilation** 要素に既存の属性があればすべて削除し、次の属性名と値を追加します。

    |属性名|属性の値|
    |--------------------|---------------------|
    |**assemblyPostProcessorType**|**Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter, Microsoft.VisualStudio.Enterprise.ASPNetHelper, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a**|

```xml
    <configuration>
        <runtime>
        . . .
        </runtime>
        <system.web>
            <compilation
                assemblyPostProcessorType="Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter,
                    Microsoft.VisualStudio.Enterprise.ASPNetHelper,
                    Version=10.0.0.0,
                    Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
            />
        </system.web>
    <configuration>
```

### <a name="to-add-profiler-location-settings-to-the-configurationappsettings-element"></a>プロファイラーの場所の設定を configuration/appSettings 要素に追加するには

1. 必要に応じて、**configuration** 要素の子要素として **appSettings** 要素を追加します。追加しない場合は次の手順に進みます。

    **appSettings** 要素には属性はありません。 **configuration** 要素には、**appSettings** 子要素を 1 つだけ含めることができます。

2. **add** 要素を **appSettings** 要素の子として追加します。

3. **add** 要素に、次の属性名と値を追加します。

   | 属性名 | 属性の値 |
   |----------------| - |
   | **key** | **Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation** |
   | **value** | `PerformanceToolsFolder` **\VSInstr.Exe** |

4. 別の **add** 要素を **appSettings** 要素の子として追加します。

5. この **add** 要素に、次の属性名と値を追加します。

   |属性名|属性の値|
   |--------------------|---------------------|
   |**key**|**Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools**|
   |**value**|`PerformanceToolsFolder`|

    `PerformanceToolsFolder` は、プロファイラーの実行可能ファイルへのパスです。 プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。

```xml
    <configuration>
        <runtime>
        . . .
        </runtime>
        . . .
        <system.web>
        </system.web>
        <appSettings>
            <add
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation"
                value="C:\Program Files\Microsoft Visual Studio 14.0\Team Tools\Performance Tools\vsinstr.exe"
        />
            <add
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools"
                value="C:\Program Files\Microsoft Visual Studio 14.0\Team Tools\Performance Tools\"
            />
        </appSettings>
    </configuration>
```

## <a name="example"></a>例
 次に示すのは、動的にコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションのインストルメント化とプロファイルを可能にする完全な *web.config* ファイルです。 この例では、変更前のファイルには他の設定が含まれていないことを前提としています。

```xml
<?xml version="1.0"?>
    <configuration>
        <runtime>
            <assemblyBinding
                xmlns="urn:schemas-microsoft-com:asm.v1"
            >
                <dependentAssembly>
                    <assemblyIdentity
                        name="Microsoft.VisualStudio.Enterprise.ASPNetHelper"
                        publicKeyToken="b03f5f7f11d50a3a"
                        culture="neutral"
                    />
                    <codeBase
                        version="10.0.0.0"
                        href="file:///C:/Program%20Files/Microsoft%20Visual%20Studio%2010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL"
                    />
                </dependentAssembly>
            </assemblyBinding>
        </runtime>
        <system.web>
            <compilation
                assemblyPostProcessorType="Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter,
                    Microsoft.VisualStudio.Enterprise.ASPNetHelper,
                    Version=10.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a"
            />
        </system.web>
        <appSettings>
            <add
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation"
                value="C:\Program Files\Microsoft Visual Studio 14.0\Team Tools\Performance Tools\vsinstr.exe"
            />
            <add
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools"
                value="C:\Program Files\Microsoft Visual Studio 14.0\Team Tools\Performance Tools\"
            />
        </appSettings>
    </configuration>

```

## <a name="see-also"></a>関連項目
- [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、詳細なタイミング データを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-app-and-collect-timing-data.md)
- [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、メモリ データを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data.md)
