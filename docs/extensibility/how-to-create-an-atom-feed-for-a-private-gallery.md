---
title: '方法 : プライベート ギャラリーの Atom フィードを作成する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c72fbf2d3973ffd84de1cf6f33788c43511c3ce4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711006"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>方法: プライベート ギャラリーの Atom フィードを作成する
拡張機能を含むイントラネットの場所に Atom (RSS) フィードを作成し、プライベート ギャラリーとして**拡張機能と更新プログラム**にフィードを追加できます。 詳細については、「プライベート[ギャラリー](../extensibility/private-galleries.md)」を参照してください。

## <a name="create-an-atom-feed"></a>Atom フィードを作成する
 Atom フィードをプライベート ギャラリーとして作成するには、まず拡張子 *(.vsix*ファイル) をフォルダに集めます。 必要に応じて、サブフォルダに整理することができます。 また、以下のリソースも必要です。

- プライベート ギャラリーとして拡張機能を使用できるようにする*atom.xml*ファイル。 *atom.xml*ファイルを**拡張機能と更新**に接続する方法については、「プライベート[ギャラリー](../extensibility/private-galleries.md)」を参照してください。

- 拡張機能から抽出されたイメージ ファイル (スクリーン ショットなど) を含むフォルダー。 *atom.xml*ファイルには、これらのイメージへの相対リンクが含まれているため、これらのイメージは**拡張機能と更新で**使用できます。

  たとえば、次の 2 つの拡張子を 1 つのフォルダにまとめたものとします。

- *Template_Wizard_239.vsix*は空の VSIX プロジェクト テンプレートです。

- *選択した*単語のすべてのインスタンスを強調表示するツールです。

  *atom.xml*ファイルの内容は、次の例のようになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title type="text" />
  <id>uuid:bcecded5-97c8-4d24-96f1-7d9e16652433;id=1</id>
  <updated>2011-04-14T21:25:48Z</updated>
  <entry>
    <id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</id>
    <title type="text">Highlight all occurrences of selected word</title>
    <summary type="text">This extends the editor to highlight ....</summary>
    <published>2011-04-14T14:24:51-07:00</published>
    <updated>2011-04-14T14:24:22-07:00</updated>
    <author>
      <name>Microsoft</name>
    </author>
    <link rel="icon" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_Icon_SelectionHighlightIcon.jpg" />
    <link rel="previewimage" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_PreviewImage_SelectionHighlight.jpg" />
    <content type="application/octet-stream" src="SelectionHighlight.vsix" />
    <Vsix xmlns="http://schemas.microsoft.com/developer/vsx-syndication-schema/2010" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</Id>
      <Version>1.31</Version>
      <References />
      <Rating xsi:nil="true" />
      <RatingCount xsi:nil="true" />
      <DownloadCount xsi:nil="true" />
    </Vsix>
  </entry>
  <entry>
    <id>Template_Wizard_239.Microsoft.3b38a7e3-5cbc-4389-a92a-d82tyc2ed592</id>
    ...
  </entry>
</feed>
```

 2 つのリンク タグは、生成されたイメージ フォルダー内のスクリーン ショットを参照していることに注意してください。

## <a name="see-also"></a>関連項目
- [プライベートギャラリー](../extensibility/private-galleries.md)
