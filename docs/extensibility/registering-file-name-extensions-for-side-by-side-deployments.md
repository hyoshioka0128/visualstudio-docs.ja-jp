---
title: サイドバイサイド Ide 用のファイル名拡張子の登録
description: サイドバイサイド配置のためにファイル名拡張子を登録する方法について説明します。これにより、ユーザーは適切なバージョンの Visual Studio でファイルを開くことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c66413890f0aaa08e09a291f5bf31a44e7c24706
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863030"
---
# <a name="register-file-name-extensions-for-side-by-side-deployments"></a>サイドバイサイド配置のためにファイル名拡張子を登録する
サイドバイサイドの環境で展開された Vspackage では、ファイル名拡張子を登録して、ファイルを正しいバージョンのに関連付ける必要があり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 バージョン固有のファイル名拡張子を使用しない限り、登録によって、ユーザーは適切なバージョンのでプロジェクトおよびプロジェクト項目ファイルを開くことができ [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

## <a name="in-this-section"></a>このセクションの内容
- [ファイル名拡張子について](../extensibility/about-file-name-extensions.md) ファイル名拡張子の登録方法について説明します。

- [ファイル名拡張子のファイルハンドラーを指定する](../extensibility/specifying-file-handlers-for-file-name-extensions.md) 特定のファイル名拡張子を開いたり、編集したりできるアプリケーションを登録する方法について説明します。

- [ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md) 動詞を登録する方法について説明します。

- [Side-by-side ファイルの関連付けの管理](../extensibility/managing-side-by-side-file-associations.md) ファイルを開くために、特定のバージョンのを呼び出すサイドバイサイドインストールを処理する方法について説明し [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

## <a name="related-sections"></a>関連項目
- [複数バージョンの Visual Studio のサポート](../extensibility/supporting-multiple-versions-of-visual-studio.md)[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]エンドユーザーへの開発およびデプロイ中に、の複数のバージョンと VSPackage に関連する問題について説明します。
