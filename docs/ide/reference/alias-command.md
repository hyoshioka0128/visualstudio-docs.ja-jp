---
title: Alias コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- tools.alias
helpviewer_keywords:
- aliases, Visual Studio commands
- commands, aliases
- Tools.Alias command
- command aliases
- alias command
ms.assetid: bdf857df-b5d5-450f-8c10-a6fd4dccc130
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 031f1a4bab1acee3f3d0999b17c0b607f7808df9
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596906"
---
# <a name="alias-command"></a>Alias コマンド
完全なコマンド、完全なコマンドと引数、または他のエイリアスに対して新しいエイリアスを作成します。

> [!TIP]
> 引数を指定せずに「`>alias`」と入力すると、現在のエイリアスとその定義が一覧表示されます。

## <a name="syntax"></a>構文

```cmd
Tools.Alias [/delete] [/reset] [aliasname] [aliasstring]
```

## <a name="arguments"></a>引数
`aliasname`\
任意。 新しいエイリアスの名前。 `aliasname` の値を指定しない場合は、現在のエイリアス一覧とその定義が表示されます。

`aliasstring`\
任意。 完全なコマンド名または既存のエイリアスと、エイリアスとして作成する任意のパラメーター。 `aliasstring` の値を指定しない場合は、指定したエイリアスの名前と文字列が表示されます。

## <a name="switches"></a>スイッチ
/delete または /del または /d\
任意。 指定したエイリアスを削除し、オート コンプリートから除外します。

/reset\
任意。 定義済みエイリアスの一覧を元の設定に戻します。 つまり、定義済みエイリアスをすべて復元し、ユーザー定義のエイリアスをすべて削除します。

## <a name="remarks"></a>解説
エイリアスはコマンドを表すため、コマンド ラインの先頭に指定する必要があります。

このコマンドを実行するときは、エイリアスの後ではなく、コマンドの直後にスイッチを置く必要があります。そうしないと、スイッチ自体がエイリアスの文字列の一部として取り込まれます。

`/reset` スイッチを指定すると、エイリアスを復元する前に確認メッセージが表示されます。 `/reset` には省略形はありません。

## <a name="examples"></a>例
次の例では、Edit.MakeUpperCase という完全なコマンドに対し、`upper` という新しいエイリアスを作成します。

```cmd
>Tools.Alias upper Edit.MakeUpperCase
```

エイリアス `upper` を削除するコードは次のとおりです。

```cmd
>Tools.alias /delete upper
```

現在のすべてのエイリアスの一覧とその定義を表示するコードは次のとおりです。

```cmd
>Tools.Alias
```

## <a name="see-also"></a>参照

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [[コマンド] ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
