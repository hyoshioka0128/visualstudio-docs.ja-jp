---
title: プロジェクト テンプレートと項目テンプレートのパラメーター
ms.date: 01/02/2018
ms.topic: reference
helpviewer_keywords:
- Visual Studio templates, parameters
- template parameters [Visual Studio]
- project templates, parameters
- item templates, parameters
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 582c87eee2586eab12f70e2d27341987e7cb7e2a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585887"
---
# <a name="template-parameters"></a>テンプレート パラメーター

テンプレートがインスタンス化されるとき、テンプレートの値を置換できます。 この機能を設定するには、*テンプレート パラメーター*を使用します。 テンプレート パラメーターは、テンプレートのクラス名や名前空間など、値を置換するために使用できます。 ユーザーが新しい項目やプロジェクトを追加したときにバックグラウンドで実行されるテンプレート ウィザードによってこれらのパラメーターが置換されます。

## <a name="declare-and-enable-template-parameters"></a>テンプレート パラメーターを宣言して有効にする

テンプレート パラメーターは、$*parameter*$ という形式で宣言されます。 次に例を示します。

- $safeprojectname$

- $guid1$

- $guid5$

### <a name="enable-parameter-substitution-in-templates"></a>テンプレートでパラメーター置換を有効にする

1. テンプレートの *.vstemplate* ファイル内で、パラメーター置換を有効にする項目に対応する `ProjectItem` 要素を見つけます。

1. `ReplaceParameters` 要素の `ProjectItem` 属性を `true` に設定します。

1. プロジェクト項目のコード ファイルで、必要に応じてパラメーターを含めます。 たとえば、次のパラメーターは、ファイル内で名前空間に対して安全なプロジェクト名が使用されることを指定します。

    ```csharp
    namespace $safeprojectname$
    ```

## <a name="reserved-template-parameters"></a>予約済みのテンプレート パラメーター

テンプレートで使用できる予約済みテンプレート パラメーターを次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|clrversion|共通言語ランタイム (CLR: Common Language Runtime) の現在のバージョン。|
|ext_*|親テンプレートの変数を参照するには、パラメーターに `ext_` プレフィックスを追加します。 たとえば、`ext_safeprojectname` のようにします。|
|guid[1-10]|プロジェクト ファイルでプロジェクト GUID を置き換えるために使用される GUID。 最大 10 個の一意 GUID を指定できます (例: `guid1`)。|
|itemname|パラメーターが使用されているファイルの名前。|
|machinename|現在のコンピューター名 (たとえば、Computer01)。|
|projectname|プロジェクトの作成時にユーザーが指定した名前。|
|registeredorganization|HKLM\Software\Microsoft\Windows NT\CurrentVersion\RegisteredOrganization のレジストリ キー値。|
|rootnamespace|現在のプロジェクトのルート名前空間。 このパラメーターは、項目テンプレートにのみ適用されます。|
|safeitemname|`itemname` と同じですが、安全でない文字とスペースはすべてアンダースコア文字に置き換えられます。|
|safeitemrootname|`safeitemname` と同じ。|
|safeprojectname|プロジェクトの作成時にユーザーによって指定された名前ですが、すべての安全でない文字およびスペースがすべて削除されています。|
|時間|DD/MM/YYYY 00:00:00 の形式で表した現在の時間。|
|specifiedSolutionName|ソリューションの名前。 [ソリューションのディレクトリを作成] がオンになっている場合は、`specifiedSolutionName` にソリューション名が指定されます。 [ソリューションのディレクトリを作成] がオフになっている場合、`specifiedSolutionName` は空白です。|
|userdomain|現在のユーザー ドメイン。|
|username|現在のユーザー名。|
|webnamespace|現在の Web サイトの名前。 このパラメーターは、Web フォーム テンプレートで一意のクラス名を保証するために使用されます。 この Web サイトが Web サーバーのルート ディレクトリにある場合、このテンプレート パラメーターは Web サーバーのルート ディレクトリとして解決されます。|
|年|YYYY の形式で表した現在の年。|

> [!NOTE]
> テンプレート パラメーターでは、大文字と小文字が区別されます。

## <a name="custom-template-parameters"></a>カスタム テンプレート パラメーター

パラメーター置換時に使われる既定の予約済みテンプレート パラメーターの他に、独自のテンプレート パラメーターと値を指定できます。 詳細については、「[CustomParameters 要素 (Visual Studio テンプレート)](../extensibility/customparameters-element-visual-studio-templates.md)」を参照してください。

## <a name="example-use-the-project-name-for-a-file-name"></a>例:ファイル名に対するプロジェクト名の使用

`TargetFileName` 属性でパラメーターを使うことにより、プロジェクト項目に対して変数ファイル名を指定できます。

次の例では、実行可能ファイルの名前でプロジェクト名 (`$projectname$` で指定されています) を使うように指定します。

```xml
<TemplateContent>
    <ProjectItem
        ReplaceParameters="true"
        TargetFileName="$projectname$.exe">
            File1.exe
    </ProjectItem>
      ...
</TemplateContent>
```

## <a name="example-use-the-safe-project-name-for-the-namespace-name"></a>例:名前空間名に対する安全なプロジェクト名の使用

C# クラス ファイルの名前空間に対して安全なプロジェクト名を使うには、次の構文を使います。

```csharp
namespace $safeprojectname$
{
    public class Class1
    {
        public Class1()
        { }
    }
}
```

プロジェクト テンプレートの *.vstemplate* ファイルで、ファイルを参照するときに `ReplaceParameters="true"` 属性を指定します。

```xml
<TemplateContent>
    <ProjectItem ReplaceParameters="true">
        Class1.cs
    </ProjectItem>
    ...
</TemplateContent>
```

## <a name="see-also"></a>関連項目

- [方法: テンプレート内のパラメーターを置き換える](how-to-substitute-parameters-in-a-template.md)
- [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)
- [方法: プロジェクト テンプレートを作成する](../ide/how-to-create-project-templates.md)
- [テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
