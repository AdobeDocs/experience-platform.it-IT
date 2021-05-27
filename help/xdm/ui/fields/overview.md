---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;campo;
solution: Experience Platform
title: Definire i campi XDM nell’interfaccia utente
description: Scopri come definire campi XDM nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 4%

---

# Definire i campi XDM nell’interfaccia utente

L’ [!DNL Schema Editor] nell’interfaccia utente di Adobe Experience Platform ti consente di definire campi personalizzati all’interno delle classi Experience Data Model (XDM) personalizzate e dei gruppi di campi dello schema. Questa guida descrive i passaggi per la definizione dei campi XDM nell’interfaccia utente, incluse le opzioni di configurazione disponibili per ciascun tipo di campo.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema Experience Platform, fai riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base sulla composizione dello schema](../../schema/composition.md) per scoprire in che modo classi e gruppi di campi contribuiscono ai campi degli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Seleziona una risorsa per aggiungere campi a {#select-resource}

Per definire nuovi campi XDM nell’interfaccia utente, devi prima aprire uno schema all’interno di [!DNL Schema Editor]. A seconda degli schemi attualmente disponibili in [!DNL Schema Library], è possibile scegliere di [creare un nuovo schema](../resources/schemas.md#create) o [selezionare uno schema esistente da modificare](../resources/schemas.md#edit).

Una volta aperta la [!DNL Schema Editor], utilizza la barra a sinistra per selezionare la classe o il gruppo di campi per cui desideri definire i campi. Se la risorsa è una risorsa personalizzata definita dall’organizzazione, i controlli per aggiungere o modificare i campi vengono visualizzati nell’area di lavoro. Tali controlli vengono visualizzati accanto al nome dello schema, nonché a tutti i campi di tipo oggetto definiti nella classe o nel gruppo di campi selezionati.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Se la classe o il gruppo di campi selezionato è una risorsa di base fornita dall’Adobe, non può essere modificata e pertanto i controlli mostrati sopra non verranno visualizzati. Se lo schema a cui si desidera aggiungere i campi si basa su una classe XDM principale e non contiene gruppi di campi personalizzati, è possibile [creare un nuovo gruppo di campi](../resources/field-groups.md#create) da aggiungere allo schema.

Per aggiungere un nuovo campo alla risorsa, seleziona l’icona **più (+)** accanto al nome dello schema nell’area di lavoro o accanto al campo del tipo di oggetto in cui si desidera definire il campo.

![](../../images/ui/fields/overview/plus-icon.png)

## Definire un campo per una risorsa {#define}

Dopo aver selezionato l&#39;icona **più (+)**, nell&#39;area di lavoro viene visualizzato un **[!UICONTROL Nuovo campo]**, situato all&#39;interno di un oggetto a livello di radice con namespace nell&#39;ID tenant univoco (mostrato come `_tenantId` nell&#39;esempio seguente). Tutti i campi aggiunti a uno schema tramite classi e gruppi di campi personalizzati vengono inseriti automaticamente in questo spazio dei nomi per evitare conflitti con altri campi delle classi e dei gruppi di campi forniti da Adobi.

![](../../images/ui/fields/overview/new-field.png)

Nella barra a destra in **[!UICONTROL Proprietà campo]**, puoi configurare i dettagli dei nuovi campi. Per ogni campo sono necessarie le seguenti informazioni:

| Proprietà campo | Descrizione |
| --- | --- |
| [!UICONTROL Nome campo] | Nome descrittivo univoco del campo. Il nome del campo non può essere modificato dopo il salvataggio dello schema.<br><br>Il nome dovrebbe idealmente essere scritto in camelCase. Può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura, ma **potrebbe non essere** iniziare con un trattino basso.<ul><li>**Corretto**:  `fieldName`</li><li>**Accettabile:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Errato**:  `_fieldName`</li></ul> |
| [!UICONTROL Nome visualizzato] | Un nome descrittivo per il campo. |
| [!UICONTROL Tipo] | Il tipo di dati che il campo conterrà. Da questo menu a discesa, è possibile selezionare uno dei [tipi scalari standard](../../schema/field-constraints.md) supportati da XDM oppure uno dei tipi di dati [a3/> a più campi definiti in precedenza in [!DNL Schema Registry].](../resources/data-types.md)<br><br>È inoltre possibile selezionare  **[!UICONTROL Ricerca tipo avanzata per]** cercare e filtrare i tipi di dati esistenti e individuare più facilmente il tipo desiderato. |

{style=&quot;table-layout:auto&quot;}

È inoltre possibile fornire al campo una **[!UICONTROL Descrizione]** leggibile da un utente opzionale per fornire più contesto riguardo al caso d’uso previsto del campo.

>[!NOTE]
>
>A seconda del **[!UICONTROL Tipo]** selezionato per il campo, nella barra a destra possono essere visualizzati controlli di configurazione aggiuntivi. Per ulteriori informazioni su questi controlli, consulta la sezione sulle [proprietà del campo specifiche per i tipi](#type-specific-properties) .
>
>La barra a destra fornisce anche delle caselle di controllo per la designazione di tipi di campi speciali. Per ulteriori informazioni, consulta la sezione sui [tipi di campi speciali](#special) .

Al termine della configurazione del campo, seleziona **[!UICONTROL Applica]**.

![](../../images/ui/fields/overview/field-details.png)

L’area di lavoro viene aggiornata in modo da visualizzare il nome e il tipo del campo. Nella barra a destra viene ora visualizzato il percorso del campo oltre alle altre proprietà.

![](../../images/ui/fields/overview/field-added.png)

Puoi continuare a seguire i passaggi descritti sopra per aggiungere altri campi allo schema. Una volta salvato lo schema, vengono salvati anche i relativi gruppi di campi e classi di base, se sono state apportate modifiche.

>[!NOTE]
>
>Eventuali modifiche apportate ai gruppi di campi o alla classe di uno schema verranno applicate a tutti gli altri schemi che li utilizzano.

## Proprietà dei campi specifiche per il tipo {#type-specific-properties}

Quando definisci un nuovo campo, nella barra a destra possono essere visualizzate opzioni di configurazione aggiuntive a seconda del **[!UICONTROL Tipo]** scelto per il campo. La tabella seguente illustra le proprietà aggiuntive dei campi insieme ai relativi tipi compatibili:

| Proprietà campo | Tipi compatibili | Descrizione |
| --- | --- | --- |
| [!UICONTROL Valore predefinito] | [!UICONTROL Stringa],  [!UICONTROL Doppio],  [!UICONTROL Lungo],  [!UICONTROL Intero],  [!UICONTROL Breve],  [!UICONTROL Byte],  [!UICONTROL Booleano] | Un valore predefinito che verrà assegnato a questo campo se durante l’acquisizione non viene fornito alcun altro valore. Questo valore deve essere conforme al tipo selezionato del campo. |
| [!UICONTROL Pattern] | [!UICONTROL Stringa] | Un&#39; [espressione regolare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) a cui il valore di questo campo deve essere conforme per essere accettato durante l&#39;acquisizione. |
| [!UICONTROL Formato] | [!UICONTROL Stringa] | Selezionare da un elenco di formati predefiniti per le stringhe a cui il valore deve essere conforme. I formati disponibili sono: <ul><li>[[!UICONTROL ora]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL e-mail]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-riferimento]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-puntatore]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Lunghezza minima] | [!UICONTROL Stringa] | Il numero minimo di caratteri che la stringa deve contenere affinché il valore possa essere accettato durante l’acquisizione. |
| [!UICONTROL Lunghezza massima] | [!UICONTROL Stringa] | Il numero massimo di caratteri che la stringa deve contenere affinché il valore possa essere accettato durante l’acquisizione. |
| [!UICONTROL Valore minimo] | [!UICONTROL Doppio] | Il valore minimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, viene accettato il valore . Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Valore minimo esclusivo]&quot; deve essere lasciato vuoto. |
| [!UICONTROL Valore massimo] | [!UICONTROL Doppio] | Il valore massimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, viene accettato il valore . Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Valore massimo esclusivo]&quot; deve essere lasciato vuoto. |
| [!UICONTROL Valore minimo esclusivo] | [!UICONTROL Doppio] | Il valore massimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, il valore viene rifiutato. Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Valore minimo]&quot; (non esclusivo) deve essere lasciato vuoto. |
| [!UICONTROL Valore massimo esclusivo] | [!UICONTROL Doppio] | Il valore massimo per il valore Double da accettare durante l’acquisizione. Se il valore acquisito corrisponde esattamente a quello inserito qui, il valore viene rifiutato. Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Valore massimo]&quot; (non esclusivo) deve essere lasciato vuoto. |

{style=&quot;table-layout:auto&quot;}

## Tipi di campi speciali {#special}

La barra a destra fornisce diverse caselle di controllo per la designazione di ruoli speciali per il campo selezionato. I casi di utilizzo per alcune di queste opzioni richiedono considerazioni importanti sulla strategia di modellazione dei dati e su come si intende utilizzare i servizi della piattaforma a valle.

Per ulteriori informazioni su questi tipi speciali, consulta la seguente documentazione:

* [[!UICONTROL Obbligatorio]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identità]](./identity.md)  (disponibile solo per i campi stringa)
* [[!UICONTROL Relazione]](./relationship.md)  (Disponibile solo per i campi stringa)

Sebbene tecnicamente non sia un tipo di campo speciale, si consiglia anche di visitare la guida sulla [definizione dei campi di tipo oggetto](./object.md) per ulteriori informazioni sulla definizione dei campi secondari nidificati nelle strutture dello schema.

## Passaggi successivi

Questa guida fornisce una panoramica sulla definizione dei campi XDM nell’interfaccia utente. Tenere presente che i campi possono essere aggiunti solo agli schemi tramite l’uso di classi e gruppi di campi. Per ulteriori informazioni su come gestire queste risorse nell&#39;interfaccia utente, consulta le guide per la creazione e la modifica di [classi](../resources/classes.md) e [gruppi di campi](../resources/field-groups.md).

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemi], consulta la panoramica dell&#39;area di lavoro [[!UICONTROL Schemi]](../overview.md).
