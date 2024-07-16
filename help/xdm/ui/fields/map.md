---
title: Definire i campi mappa nell’interfaccia utente
description: Scopri come definire un campo mappa nell’interfaccia utente di Experience Platform.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: ee27fc42a1ee23ef650d320df64e5970a84d0d38
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Definire i campi mappa nell’interfaccia utente

Adobe Experience Platform consente di personalizzare completamente la struttura delle classi XDM (Experience Data Model) personalizzate, dei gruppi di campi dello schema e dei tipi di dati.

Nell’Editor schema puoi anche definire i campi mappa per modellare strutture di dati flessibili e dinamiche o archiviare una raccolta di coppie chiave-valore.

Quando definisci un nuovo campo nell&#39;interfaccia utente di Platform, utilizza il menu a discesa **[!UICONTROL Tipo]** e seleziona &quot;**[!UICONTROL Mappa]**&quot; dall&#39;elenco.

![Editor schemi con elenco a discesa Tipo e valore mappa evidenziato.](../../images/ui/fields/special/map.png)

Viene visualizzata una proprietà [!UICONTROL Map value type]. Questo valore è richiesto per i tipi di dati [!UICONTROL Map]. I valori disponibili per la mappa sono [!UICONTROL String] e [!UICONTROL Integer]. Seleziona un valore dall’elenco a discesa delle opzioni disponibili.

![Editor schemi con elenco a discesa [!UICONTROL Tipo di valore mappa] evidenziato.](../../images/ui/fields/special/map-value-type.png)

Dopo aver configurato il sottocampo, è necessario assegnarlo a un gruppo di campi. Utilizza il menu a discesa **[!UICONTROL Gruppo di campi]** o il campo di ricerca e seleziona **[!UICONTROL Applica]**. Puoi continuare ad aggiungere campi all&#39;oggetto utilizzando lo stesso processo oppure selezionare **[!UICONTROL Salva]** per confermare le impostazioni.

![Registrazione della selezione del gruppo di campi e delle impostazioni applicate.](../../images/ui/fields/special/assign-to-field-group.gif)

## Limitazioni di utilizzo {#restrictions}

XDM pone le seguenti restrizioni sull’utilizzo di questo tipo di dati:

* I tipi di mappa DEVONO essere di tipo `object`.
* I tipi di mappa NON DEVONO avere proprietà definite (in altre parole, definiscono oggetti &quot;vuoti&quot;).
* I tipi di mappa DEVONO includere un campo `additionalProperties.type` che descrive i valori che possono essere inseriti nella mappa, `string` o `integer`.
* La segmentazione multi-entità può essere definita solo in base alle chiavi della mappa e non ai valori.
* Le mappe non sono supportate per i tipi di pubblico dell’account.

Assicurati di utilizzare campi di tipo mappa solo quando assolutamente necessario, in quanto presentano i seguenti svantaggi in termini di prestazioni:

* Il tempo di risposta di [Adobe Experience Platform Query Service](../../../query-service/home.md) diminuisce da tre a dieci secondi per 100 milioni di record.
* Le mappe devono avere meno di 16 chiavi altrimenti si rischia un ulteriore degrado.

>[!NOTE]
>
>L’interfaccia utente di Platform presenta limitazioni su come estrarre le chiavi dei campi di tipo mappa. Mentre i campi di tipo oggetto possono essere espansi, le mappe vengono visualizzate come un singolo campo. I campi di mapping creati tramite l&#39;API Schema Registry che non sono tipi di dati stringa o interi vengono visualizzati come tipi di dati &quot;[!UICONTROL Complex]&quot;.

## Passaggi successivi

Dopo aver letto questo documento, ora puoi definire i campi mappa nell’interfaccia utente di Platform. È possibile utilizzare solo classi e gruppi di campi per aggiungere campi agli schemi. Per ulteriori informazioni su come gestire queste risorse nell&#39;interfaccia utente, consulta le guide sulla creazione e la modifica di [classi](../resources/classes.md) e [gruppi di campi](../resources/field-groups.md).

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemi], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemi]](../overview.md).
