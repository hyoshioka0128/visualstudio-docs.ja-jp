---
title: アセンブリ要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio templates]
- <Assembly> element [Visual Studio templates]
ms.assetid: 9242f76a-1273-4b8a-8f26-6606f91829ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c80044657b16448ba4567fff839274226985fa14
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740035"
---
# <a name="assembly-element-visual-studio-templates"></a>アセンブリ要素
テンプレートが、そのアセンブリの参照をプロジェクトに追加するために使用する、アセンブリに関する情報を指定します。

 \<VSTemplate \<> テンプレート\<コンテンツ>\<アセンブリ>>参照>参照\<

## <a name="syntax"></a>構文

```
<Assembly> AssemblyName </Assembly>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[リファレンス](../extensibility/reference-element-visual-studio-templates.md)|項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、項目テンプレートがインスタンス化されるときにプロジェクトに追加するアセンブリを指定します。 このアセンブリ名は、次のいずれかの方法で指定する必要があります。

- 完全なアセンブリ名として使用します。 次に例を示します。

    ```
    <Assembly>
        MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom = null.
    </Assembly>
    ```

- 単純なテキストリファレンスとして。 次に例を示します。

    ```
    <Assembly> System </Assembly>
    ```

## <a name="remarks"></a>Remarks
 `Assembly` は `Reference` に必須の子要素です。

 および`Reference``References,``Type``Item`要素は、属性値が *.vstemplate*ファイルの場合にのみ使用できます。 `Assembly`

## <a name="example"></a>例
 項目テンプレートの要素を`TemplateContent`次の例に示します。 この XML は *、System.dll*アセンブリおよび*System.Data.dll*アセンブリへの参照を追加します。

```
<TemplateContent>
    <References>
        <Reference>
            <Assembly>
                System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
        <Reference>
            <Assembly>
                System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
    </References>
    ...
</TemplateContent>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
