---
title: Flusso per estensioni Edge
description: Scopri in che modo i componenti di un’estensione edge in Adobe Experience Platform interagiscono tra loro in fase di runtime.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 85%

---

# Flusso per estensioni Edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch è ora una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nelle estensioni edge, ogni condizione, azione e tipo di elemento dati dispone di una vista mediante la quale gli utenti possono modificare le impostazioni e di un modulo libreria che agisce in base alle impostazioni definite dall&#39;utente.

Come mostra il diagramma di alto livello riportato di seguito, la vista del tipo di evento dell&#39;estensione verrà visualizzata all&#39;interno di un iframe nell&#39;applicazione integrata con Adobe Experience Platform. La vista viene quindi utilizzata per modificare le impostazioni che vengono quindi salvate in Experience Platform. Quando viene generata la libreria runtime di tag, sia il modulo libreria dei tipi di azioni dell’estensione che le impostazioni definite dall’utente vengono inclusi nella libreria di runtime che viene distribuita al nodo edge. Le impostazioni definite dall’utente da Experience Platform vengono inserite nel modulo libreria in fase di esecuzione.

![diagramma del flusso per le estensioni](../images/flow/edge/event-processing-flow.png)

Il seguente diagramma illustra il collegamento tra eventi, condizioni e azioni all’interno del flusso di elaborazione delle regole.

![diagramma del flusso di elaborazione delle regole](../images/flow/edge/rule-processing-flow.png)

Il flusso di elaborazione delle regole comprende le seguenti fasi:

1. All’avvio, i metodi `settings` e `trigger` vengono trasmessi al modulo libreria di eventi.
1. Quando il modulo libreria degli eventi determina che si è verificato un determinato evento, viene richiamato `trigger`.
1. Experience Platform trasmette `settings` nei moduli libreria delle condizioni della regola in cui vengono valutate le condizioni.
1. Ogni tipo di condizione restituisce se una condizione è stata valutata &quot;true&quot;.
1. Se tutte le condizioni risultano “true”, le azioni della regola vengono eseguite.
