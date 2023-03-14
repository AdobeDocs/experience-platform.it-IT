---
title: Flusso per estensioni web
description: Scopri come i componenti di estensione web interagiscono tra loro in fase di runtime in Adobe Experience Platform.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 93%

---

# Flusso per estensioni web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [document](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Ogni evento, condizione, azione e tipo di elemento dati nelle estensioni Web dispone di una vista mediante la quale gli utenti possono modificare le impostazioni e di un modulo libreria che agisce in base alle impostazioni definite dall&#39;utente.

Come mostra il diagramma di alto livello riportato di seguito, la vista del tipo di evento dell’estensione verrà visualizzata all’interno di un iframe nell’applicazione integrata con Adobe Experience Platform. L’utente utilizza questa vista per modificare le impostazioni che vengono quindi salvate in Platform. Quando viene generata la libreria runtime di tag, vengono inclusi sia il modulo libreria dei tipi di evento dell’estensione sia le impostazioni definite dall’utente. In fase di runtime, Platform inserisce le impostazioni definite dall’utente nel modulo libreria.

![diagramma del flusso per le estensioni](../images/flow/web/extension-flow.png)

Il seguente diagramma illustra il collegamento tra eventi, condizioni e azioni all’interno del flusso di elaborazione delle regole.

![diagramma del flusso di elaborazione delle regole](../images/flow/web/rule-processing-flow.png)

Il flusso di elaborazione delle regole comprende le seguenti fasi:

1. All’avvio, i metodi `settings` e `trigger` vengono trasmessi al modulo libreria di eventi.
1. Quando il modulo libreria degli eventi determina che si è verificato un determinato evento, viene richiamato `trigger`.
1. I tag trasmettono `settings` nei moduli libreria delle condizioni della regola in cui vengono valutate le condizioni.
1. Ogni modulo libreria di condizioni restituisce se una condizione è stata valutata “true”.
1. Se tutte le condizioni risultano “true”, le azioni della regola vengono eseguite.
