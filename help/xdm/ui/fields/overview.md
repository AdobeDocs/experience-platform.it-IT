---
keywords: ' Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;area di lavoro;campo;'
solution: Experience Platform
title: Definire i campi XDM nell'interfaccia utente
description: Scoprite come definire i campi XDM nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 70b3ad788dd78c6100782869e3065cc17a54ece1
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 3%

---


# Definire i campi XDM nell&#39;interfaccia utente

La [!DNL Schema Editor] nell&#39;interfaccia utente di Adobe Experience Platform consente di definire i propri campi all&#39;interno delle classi e dei mixin personalizzati di Experience Data Model (XDM). Questa guida illustra i passaggi necessari per definire i campi XDM nell&#39;interfaccia utente, incluse le opzioni di configurazione disponibili per ciascun tipo di campo.

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Fare riferimento alla [Panoramica XDM](../../home.md) per un&#39;introduzione al ruolo di XDM nell&#39;ecosistema  Experience Platform, e alle [nozioni di base della composizione dello schema](../../schema/composition.md) per scoprire in che modo classi e mixin contribuiscono ai campi degli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire dimestichezza con le diverse funzionalità di [!DNL Schema Editor].

## Selezionare una risorsa per aggiungere campi a {#select-resource}

Per definire nuovi campi XDM nell&#39;interfaccia utente, è innanzitutto necessario aprire uno schema all&#39;interno di [!DNL Schema Editor]. A seconda degli schemi attualmente disponibili in [!DNL Schema Library], è possibile scegliere di [creare un nuovo schema](../resources/schemas.md#create) o [selezionare uno schema esistente da modificare](../resources/schemas.md#edit).

Una volta aperta la [!DNL Schema Editor], utilizzate la barra a sinistra per selezionare la classe o il mixin per il quale desiderate definire i campi. Se la risorsa è una risorsa personalizzata definita dall&#39;organizzazione, nell&#39;area di lavoro sono visualizzati i controlli per l&#39;aggiunta o la modifica dei campi. Tali controlli vengono visualizzati accanto al nome dello schema, nonché a tutti i campi del tipo di oggetto definiti nella classe o nel mixin selezionato.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Se la classe o il mixin selezionato è una risorsa di base fornita da  Adobe, non può essere modificato e quindi i controlli riportati sopra non verranno visualizzati. Se lo schema a cui si desidera aggiungere i campi è basato su una classe XDM di base e non contiene mixin personalizzati, è possibile [creare un nuovo mixin](../resources/mixins.md#create) da aggiungere allo schema.

Per aggiungere un nuovo campo alla risorsa, selezionare l&#39;icona **più (+)** accanto al nome dello schema nel quadro oppure accanto al campo del tipo di oggetto in cui si desidera definire il campo.

![](../../images/ui/fields/overview/plus-icon.png)

## Definire un campo per una risorsa {#define}

Dopo aver selezionato l&#39;icona **più (+)**, nell&#39;area di lavoro viene visualizzato un **[!UICONTROL New field]**, situato all&#39;interno di un oggetto a livello principale che viene associato all&#39;ID tenant univoco (come `_tenantId` nell&#39;esempio seguente). Tutti i campi aggiunti a uno schema tramite classi e mixin personalizzati vengono inseriti automaticamente all&#39;interno di questo spazio nomi per evitare conflitti con altri campi da  classi e mixin forniti dal Adobe.

![](../../images/ui/fields/overview/new-field.png)

Nella barra a destra in **[!UICONTROL Field properties]**, puoi configurare i dettagli dei nuovi campi. Per ogni campo sono necessarie le seguenti informazioni:

| Proprietà field | Descrizione |
| --- | --- |
| [!UICONTROL Field name] | Un nome univoco e descrittivo per il campo. Il nome del campo non può essere modificato dopo il salvataggio dello schema.<br><br>Il nome deve essere scritto idealmente in camelCase. Può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura, ma non **può iniziare con un carattere di sottolineatura.**<ul><li>**Corretto**:  `fieldName`</li><li>**Accettabile:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Scorretto**:  `_fieldName`</li></ul> |
| [!UICONTROL Display name] | Un nome descrittivo per il campo. |
| [!UICONTROL Type] | Il tipo di dati che il campo conterrà. Da questo menu a discesa, è possibile selezionare uno dei [tipi scalari standard](../../schema/field-constraints.md) supportati da XDM, o uno dei tipi di dati multi-campo [](../resources/data-types.md) precedentemente definiti in [!DNL Schema Registry].<br><br>È inoltre possibile selezionare  **[!UICONTROL Advanced type search]** per cercare e filtrare i tipi di dati esistenti e individuare più facilmente il tipo desiderato. |

È inoltre possibile fornire al campo un **[!UICONTROL Description]** leggibile dall&#39;utente opzionale per fornire un contesto più ampio in merito al caso di utilizzo previsto per il campo.

>[!NOTE]
>
>A seconda della **[!UICONTROL Type]** selezionata per il campo, nella barra a destra potrebbero essere visualizzati controlli di configurazione aggiuntivi. Per ulteriori informazioni su questi controlli, vedere la sezione relativa alle [proprietà del campo specifiche del tipo](#type-specific-properties).
>
>La barra a destra include anche le caselle di controllo per la designazione di tipi di campi speciali. Per ulteriori informazioni, vedere la sezione relativa ai [tipi di campo speciali](#special).

Dopo aver configurato il campo, selezionare **[!UICONTROL Apply]**.

![](../../images/ui/fields/overview/field-details.png)

Il quadro viene aggiornato per mostrare il nome e il tipo del campo, mentre la barra a destra elenca il percorso del campo oltre alle altre proprietà.

![](../../images/ui/fields/overview/field-added.png)

È possibile continuare a seguire i passaggi descritti sopra per aggiungere altri campi allo schema. Una volta salvato lo schema, vengono salvati anche la relativa classe di base e i mixin, se sono state apportate modifiche.

>[!NOTE]
>
>Eventuali modifiche apportate ai mixin o alla classe di uno schema si rifletteranno su tutti gli altri schemi che li utilizzano.

## Proprietà dei campi specifici per il tipo {#type-specific-properties}

Durante la definizione di un nuovo campo, nella barra a destra possono essere visualizzate opzioni di configurazione aggiuntive, a seconda della **[!UICONTROL Type]** scelta per il campo. Nella tabella seguente sono illustrate le proprietà aggiuntive dei campi insieme ai tipi compatibili:

| Proprietà field | Tipi compatibili | Descrizione |
| --- | --- | --- |
| [!UICONTROL Default value] | [!UICONTROL String], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Integer], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolean] | Un valore predefinito che verrà assegnato a questo campo se durante l&#39;assimilazione non viene fornito nessun altro valore. Questo valore deve essere conforme al tipo selezionato del campo. |
| [!UICONTROL Pattern] | [!UICONTROL String] | Un&#39; [espressione regolare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) a cui il valore di questo campo deve essere conforme per essere accettato durante l&#39;assimilazione. |
| [!UICONTROL Format] | [!UICONTROL String] | Selezionare da un elenco di formati predefiniti per le stringhe a cui il valore deve essere conforme. I formati disponibili includono: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | Il numero minimo di caratteri che la stringa deve contenere affinché il valore venga accettato durante l&#39;assimilazione. |
| [!UICONTROL Maximum length] | [!UICONTROL String] | Il numero massimo di caratteri che la stringa deve contenere affinché il valore venga accettato durante l&#39;assimilazione. |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | Il valore minimo per il valore Double da accettare durante l&#39;assimilazione. Se il valore assimilato corrisponde esattamente a quello immesso qui, il valore viene accettato. Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Exclusive minimum value]&quot; deve essere lasciato vuoto. |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | Il valore massimo per il valore Double da accettare durante l&#39;assimilazione. Se il valore assimilato corrisponde esattamente a quello immesso qui, il valore viene accettato. Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Exclusive maximum value]&quot; deve essere lasciato vuoto. |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | Il valore massimo per il valore Double da accettare durante l&#39;assimilazione. Se il valore assimilato corrisponde esattamente a quello immesso qui, il valore viene rifiutato. Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Minimum value]&quot; (non esclusivo) deve essere lasciato vuoto. |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | Il valore massimo per il valore Double da accettare durante l&#39;assimilazione. Se il valore assimilato corrisponde esattamente a quello immesso qui, il valore viene rifiutato. Quando si utilizza questo vincolo, il vincolo &quot;[!UICONTROL Maximum value]&quot; (non esclusivo) deve essere lasciato vuoto. |

## Tipi di campi speciali {#special}

Nella barra a destra sono disponibili diverse caselle di controllo per la designazione di ruoli speciali per il campo selezionato. I casi di utilizzo per alcune di queste opzioni comportano importanti considerazioni sulla strategia di modellazione dei dati e sulle modalità di utilizzo dei servizi della piattaforma a valle.

Per ulteriori informazioni su questi tipi speciali, consulta la seguente documentazione:

* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) (Disponibile solo per i campi stringa)
* [[!UICONTROL Relationship]](./relationship.md) (Disponibile solo per i campi stringa)

Sebbene tecnicamente non sia un tipo di campo speciale, si consiglia anche di consultare la guida sulla [definizione di campi di tipo oggetto](./object.md) per ulteriori informazioni sulla definizione di sottomoduli nidificati in caso di struttura dello schema.

## Passaggi successivi

Questa guida fornisce una panoramica su come definire i campi XDM nell&#39;interfaccia utente. Tenere presente che i campi possono essere aggiunti solo agli schemi tramite l&#39;uso di classi e mixin. Per ulteriori informazioni sulla gestione di queste risorse nell&#39;interfaccia utente, consulta le guide per la creazione e la modifica di [classi](../resources/classes.md) e [mixins](../resources/mixins.md).

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](../overview.md).