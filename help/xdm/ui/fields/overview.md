---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;campo;
solution: Experience Platform
title: Definire i campi XDM nell’interfaccia utente
description: Scopri come definire campi XDM nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 1d4eba9f566dc1926afd7886c6ad2808ed91ea13
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 4%

---

# Definire i campi XDM nell’interfaccia utente

La [!DNL Schema Editor] nell’interfaccia utente di Adobe Experience Platform puoi definire campi personalizzati all’interno delle classi Experience Data Model (XDM) personalizzate e dei gruppi di campi dello schema. Questa guida descrive i passaggi per la definizione dei campi XDM nell’interfaccia utente, incluse le opzioni di configurazione disponibili per ciascun tipo di campo.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Fai riferimento a [Panoramica di XDM](../../home.md) introduzione al ruolo di XDM nell&#39;ecosistema Experience Platform e [nozioni di base sulla composizione dello schema](../../schema/composition.md) per scoprire come le classi e i gruppi di campi contribuiscono ai campi degli schemi XDM.

Sebbene non sia richiesto per questa guida, è consigliabile seguire anche l’esercitazione su [composizione di uno schema nell’interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità del [!DNL Schema Editor].

## Selezionare una risorsa a cui aggiungere campi {#select-resource}

Per definire nuovi campi XDM nell’interfaccia utente, devi prima aprire uno schema all’interno della [!DNL Schema Editor]. A seconda degli schemi attualmente disponibili nel [!DNL Schema Library], puoi scegliere di [creare un nuovo schema](../resources/schemas.md#create) o [selezionare uno schema esistente da modificare](../resources/schemas.md#edit).

Una volta che hai [!DNL Schema Editor] aperti, i controlli per aggiungere o modificare i campi vengono visualizzati nell’area di lavoro. Tali controlli vengono visualizzati accanto al nome dello schema, nonché a tutti i campi di tipo oggetto definiti nella classe o nel gruppo di campi selezionati.

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Se si tenta di aggiungere un campo a un oggetto fornito da un gruppo di campi standard, tale gruppo di campi verrà convertito in un gruppo di campi personalizzato e il gruppo di campi originale non sarà più disponibile. Vedi la sezione su [aggiunta di campi ai gruppi di campi standard](../resources/schemas.md#custom-fields-for-standard-groups) per ulteriori informazioni, consulta la guida dell’interfaccia utente di schemas .

Per aggiungere un nuovo campo alla risorsa, seleziona la **più (+)** accanto al nome dello schema nell’area di lavoro o accanto al campo di tipo oggetto in cui si desidera definire il campo.

![](../../images/ui/fields/overview/plus-icon.png)

A seconda che si stia aggiungendo un campo direttamente a uno schema o ai relativi gruppi di campi e classi costituenti, i passaggi necessari per aggiungere il campo variano. Il resto del documento illustra come configurare le proprietà di un campo indipendentemente da dove viene visualizzato nello schema. Per ulteriori informazioni sui diversi modi in cui i campi possono essere aggiunti a uno schema, consulta le sezioni seguenti nella guida dell’interfaccia utente degli schemi:

* [Aggiungi campi ai gruppi di campi](../resources/schemas.md#add-fields)
* [Aggiunta di campi direttamente a uno schema](../resources/schemas.md#add-individual-fields)

## Definire le proprietà di un campo {#define}

Dopo aver selezionato la **più (+)** icona, un **[!UICONTROL Nuovo campo]** viene visualizzato nell’area di lavoro, all’interno di un oggetto con namespace nell’ID tenant univoco (mostrato come `_tenantId` nell&#39;esempio seguente). Tutti i campi personalizzati aggiunti a uno schema vengono inseriti automaticamente all’interno di questo spazio dei nomi per evitare conflitti con altri campi delle classi e dei gruppi di campi forniti dall’Adobe.

![](../../images/ui/fields/overview/new-field.png)

Nella barra a destra sotto **[!UICONTROL Proprietà campo]**, puoi configurare i dettagli del nuovo campo. Per ogni campo sono necessarie le seguenti informazioni:

| Proprietà campo | Descrizione |
| --- | --- |
| [!UICONTROL Nome campo] | Nome descrittivo univoco del campo. Il nome del campo non può essere modificato dopo il salvataggio dello schema.<br><br>Il nome dovrebbe idealmente essere scritto in camelCase. Può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura, ma **non possono** inizia con un carattere di sottolineatura.<ul><li>**Corretto**: `fieldName`</li><li>**Accettabile:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Errato**: `_fieldName`</li></ul> |
| [!UICONTROL Nome visualizzato] | Un nome descrittivo per il campo. |
| [!UICONTROL Tipo] | Il tipo di dati che il campo conterrà. Da questo menu a discesa, puoi selezionare uno dei [tipi scalari standard](../../schema/field-constraints.md) supportato da XDM o da uno dei campi multipli [tipi di dati](../resources/data-types.md) definiti in precedenza nella [!DNL Schema Registry].<br><br>Puoi anche selezionare **[!UICONTROL Ricerca avanzata del tipo]** per cercare e filtrare i tipi di dati esistenti e individuare più facilmente il tipo desiderato. |

{style=&quot;table-layout:auto&quot;}

È inoltre possibile fornire un&#39;opzione leggibile dall&#39;utente **[!UICONTROL Descrizione]** al campo per fornire più contesto riguardo al caso d’uso previsto del campo.

>[!NOTE]
>
>A seconda del **[!UICONTROL Tipo]** selezionati per il campo, ulteriori controlli di configurazione possono essere visualizzati nella barra a destra. Vedi la sezione su [proprietà del campo specifiche del tipo](#type-specific-properties) per ulteriori informazioni su questi controlli.
>
>La barra a destra fornisce anche delle caselle di controllo per la designazione di tipi di campi speciali. Vedi la sezione su [tipi di campi speciali](#special) per ulteriori informazioni.

Al termine della configurazione del campo, seleziona **[!UICONTROL Applica]**.

![](../../images/ui/fields/overview/field-details.png)

L’area di lavoro viene aggiornata in modo da visualizzare il nome e il tipo del campo. Nella barra a destra viene ora visualizzato il percorso del campo oltre alle altre proprietà.

![](../../images/ui/fields/overview/field-added.png)

Puoi continuare a seguire i passaggi descritti sopra per aggiungere altri campi allo schema. Una volta salvato lo schema, vengono salvati anche i relativi gruppi di campi e classi di base, se sono state apportate modifiche.

>[!NOTE]
>
>Eventuali modifiche apportate ai gruppi di campi o alla classe di uno schema verranno applicate a tutti gli altri schemi che li utilizzano.

## Proprietà dei campi specifiche per il tipo {#type-specific-properties}

Quando definisci un nuovo campo, nella barra a destra possono essere visualizzate opzioni di configurazione aggiuntive, a seconda della **[!UICONTROL Tipo]** scegli il campo. La tabella seguente illustra le proprietà aggiuntive dei campi insieme ai relativi tipi compatibili:

| Proprietà campo | Tipi compatibili | Descrizione |
| --- | --- | --- |
| [!UICONTROL Valore predefinito] | [!UICONTROL Stringa], [!UICONTROL Doppio], [!UICONTROL Lunga], [!UICONTROL Intero], [!UICONTROL Breve], [!UICONTROL Byte], [!UICONTROL Booleano] | Un valore predefinito che verrà assegnato a questo campo se durante l’acquisizione non viene fornito alcun altro valore. Questo valore deve essere conforme al tipo selezionato del campo. |
| [!UICONTROL Pattern] | [!UICONTROL Stringa] | A [espressione regolare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) che il valore di questo campo deve essere conforme per essere accettato durante l’acquisizione. |
| [!UICONTROL Formato] | [!UICONTROL Stringa] | Selezionare da un elenco di formati predefiniti per le stringhe a cui il valore deve essere conforme. I formati disponibili sono: <ul><li>[[!UICONTROL ora]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL e-mail]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-riferimento]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-puntatore]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Lunghezza minima] | [!UICONTROL Stringa] | Il numero minimo di caratteri che la stringa deve contenere affinché il valore possa essere accettato durante l’acquisizione. |
| [!UICONTROL Lunghezza massima] | [!UICONTROL Stringa] | Il numero massimo di caratteri che la stringa deve contenere affinché il valore possa essere accettato durante l’acquisizione. |
| [!UICONTROL Valore minimo] | [!UICONTROL Doppio] | Il valore minimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, viene accettato il valore . Quando si utilizza questo vincolo, il valore &quot;[!UICONTROL Valore minimo esclusivo]&quot; vincolo deve essere lasciato vuoto. |
| [!UICONTROL Valore massimo] | [!UICONTROL Doppio] | Il valore massimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, viene accettato il valore . Quando si utilizza questo vincolo, il valore &quot;[!UICONTROL Valore massimo esclusivo]&quot; vincolo deve essere lasciato vuoto. |
| [!UICONTROL Valore minimo esclusivo] | [!UICONTROL Doppio] | Il valore massimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, il valore viene rifiutato. Quando si utilizza questo vincolo, il valore &quot;[!UICONTROL Valore minimo]&quot; (non esclusivo) il vincolo deve essere lasciato vuoto. |
| [!UICONTROL Valore massimo esclusivo] | [!UICONTROL Doppio] | Il valore massimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, il valore viene rifiutato. Quando si utilizza questo vincolo, il valore &quot;[!UICONTROL Valore massimo]&quot; (non esclusivo) il vincolo deve essere lasciato vuoto. |

{style=&quot;table-layout:auto&quot;}

## Tipi di campi speciali {#special}

La barra a destra fornisce diverse caselle di controllo per la designazione di ruoli speciali per il campo selezionato. I casi di utilizzo per alcune di queste opzioni richiedono considerazioni importanti sulla strategia di modellazione dei dati e su come si intende utilizzare i servizi della piattaforma a valle.

Per ulteriori informazioni su questi tipi speciali, consulta la seguente documentazione:

* [[!UICONTROL Obbligatorio]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identità]](./identity.md) (Disponibile solo per i campi stringa)
* [[!UICONTROL Relazione]](./relationship.md) (Disponibile solo per i campi stringa)

Anche se tecnicamente non è un tipo di campo speciale, si consiglia anche di visitare la guida su [definizione dei campi di tipo oggetto](./object.md) per ulteriori informazioni sulla definizione dei campi secondari nidificati nelle strutture dello schema.

## Passaggi successivi

Questa guida fornisce una panoramica sulla definizione dei campi XDM nell’interfaccia utente. Tenere presente che i campi possono essere aggiunti solo agli schemi tramite l’uso di classi e gruppi di campi. Per ulteriori informazioni su come gestire queste risorse nell’interfaccia utente, consulta le guide per la creazione e la modifica [classi](../resources/classes.md) e [gruppi di campi](../resources/field-groups.md).

Per ulteriori informazioni sulle funzionalità del [!UICONTROL Schemi] area di lavoro, vedi [[!UICONTROL Schemi] panoramica dell&#39;area di lavoro](../overview.md).
