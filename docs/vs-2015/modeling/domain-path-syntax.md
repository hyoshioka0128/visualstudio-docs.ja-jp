---
title: ドメインパス構文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, domain path
ms.assetid: 945994f9-72b9-42e0-81b2-e5fb3d0e282d
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4b25b47b5b711f09334501ed21abf06cb66402b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669737"
---
# <a name="domain-path-syntax"></a>ドメイン パス構文
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL 定義は XPath に似た構文を使用して、モデル内の特定の要素を見つけます。

 通常、この構文を直接扱う必要はありません。 DSL 詳細またはプロパティ ウィンドウで、下向き矢印をクリックし、パス エディターを使用できます。 ただし、パスがこの形式でフィールドに表示されるのは、エディターを使用した後です。

 ドメイン パスは次のような形式になります。

 *RelationshipName.PropertyName/!Role*

 ![CommentReferencesSubjects 参照リレーションシップ](../modeling/media/dsl-reference.png "dsl_reference")

 構文はモデルのツリーを走査します。 たとえば、上の図のように、ドメインリレーションシップに関する **コメント** を示すトピックには、 **サブジェクト** ロールがあります。 パスセグメント **/!Subjectt** は、 **サブジェクト** ロールを介してアクセスされる要素でパスが終了することを指定します。

 各セグメントの先頭はドメイン リレーションシップの名前になっています。 要素からリレーションシップへの走査の場合、パスセグメントは *relationship. PropertyName*として表示されます。 ホップが要素へのリンクからのものである場合、パスセグメントは Relationship/! として表示されます *。RoleName*。

 スラッシュはパスの構文を区切ります。 各パス セグメントは要素からリンク (リレーションシップのインスタンス) へのホップか、リンクから要素へのホップのどちらかです。 パス セグメントは多くの場合、ペアで表示されます。 1 つのパス セグメントは要素からリンクへのホップを表し、次のセグメントはリンクから他端の要素へのホップを表します。 (どのリンクもリレーションシップ自体のソースまたはターゲットになりえます)。

 要素からリンクへのホップに対して使用する名前はロールの `Property Name` の値です。 リンクから要素へのホップに対して使用する名前はターゲットのロール名です。

## <a name="see-also"></a>参照
 [モデル、クラス、およびリレーションシップについて](../modeling/understanding-models-classes-and-relationships.md)
