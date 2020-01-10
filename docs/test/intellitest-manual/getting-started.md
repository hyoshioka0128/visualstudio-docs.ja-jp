---
title: IntelliTest の概要
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Get started
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 113233c985053cfe838f385a36ec59cc211bfcb9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591659"
---
# <a name="get-started-with-microsoft-intellitest"></a>Microsoft IntelliTest の概要

* IntelliTest を初めて使用する場合
  * [Channel 9 ビデオ](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Intellitest)を見る
  * この [MSDN マガジンに記載されている概要](https://msdn.microsoft.com/magazine/dn904672.aspx)を読む
  * Microsoft の[ドキュメント](../../test/generate-unit-tests-for-your-code-with-intellitest.md)を読む
* [Stack Overflow](https://stackoverflow.com/questions/tagged/intellitest) で質問する
* このリファレンス マニュアルの残りの部分を読む
* クイック リファレンスのこのページを印刷する

## <a name="important-attributes"></a>重要な属性

* [PexClass](attribute-glossary.md#pexclass): **PUT** を含む型をマークします。
* [PexMethod](attribute-glossary.md#pexmethod): **PUT** をマークします。
* [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull): null 以外のパラメーターをマークします。

```csharp
using Microsoft.Pex.Framework;

[..., PexClass(typeof(Foo))]
public partial class FooTest {
    [PexMethod]
    public void Bar([PexAssumeNotNull]Foo target, int i) {
        target.Bar(i);
    }
}
```

* [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest): テスト プロジェクトをプロジェクトにバインドします。
* [PexInstrumentAssembly](attribute-glossary.md#pexinstrumentassemblyattribute): インストルメント化するアセンブリを指定します。

```csharp
[assembly: PexAssemblyUnderTest("MyAssembly")] // also instruments "MyAssembly"
[assembly: PexInstrumentAssembly("Lib")]
```

## <a name="helper-classes"></a> 重要な静的ヘルパー クラス

* [PexAssume](static-helper-classes.md#pexassume): 前提事項 (入力フィルター) を評価します。
* [PexAssert](static-helper-classes.md#pexassert): アサーションを評価します。
* [PexChoose](static-helper-classes.md#pexchoose): 新しい選択項目 (追加入力) を生成します。
* [PexObserve](static-helper-classes.md#pexobserve): ライブ値を生成されたテストに記録します。

```csharp
[PexMethod]
void StaticHelpers(Foo target) {
    PexAssume.IsNotNull(target);

    int i = PexChoose.Value<int>("i");
    string result = target.Bar(i);

    PexObserve.ValueForViewing<string>("result", result);
    PexAssert.IsNotNull(result);
}
```

## <a name="got-feedback"></a>フィードバックをお寄せください

ご意見や機能に関するご要望を[開発者コミュニティ](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)で投稿してください。
