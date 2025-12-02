---
title: Guida introduttiva all’estensione tag Web SDK
description: Invia i dati dell’evento a Adobe Experience Platform Edge Network utilizzando l’estensione tag Web SDK.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Guida introduttiva all’estensione tag Web SDK

Utilizza i **tag** di Adobe Experience Platform (precedentemente Launch) per inviare i dati dell&#39;evento dal tuo sito Web alle soluzioni Edge Network e Adobe a valle.

Prima di seguire questi passaggi, assicurati di poter accedere ai seguenti [diritti di proprietà](/help/tags/ui/administration/user-permissions.md):

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Inoltre, assicurati di disporre di tutte le [autorizzazioni](/help/access-control/home.md#permissions) nelle seguenti categorie:

* Modellazione dati
* Identità

## Creare uno schema XDM {#schema}

[Experience Data Model (XDM)](/help/xdm/home.md) è una specifica open-source che fornisce strutture e definizioni comuni per i dati sotto forma di schemi. La configurazione di uno schema è vivamente consigliata per l’invio di dati ad Edge Network.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Seleziona **[!UICONTROL Create schema]**.
1. Seleziona **[!UICONTROL Experience Event]**, quindi seleziona **[!UICONTROL Next]**.
1. Assegnare allo schema un nome desiderato, quindi selezionare **[!UICONTROL Finish]**.
1. (Facoltativo) Puoi aggiungere altri campi o [gruppi di campi](/help/xdm/ui/resources/field-groups.md) per qualsiasi dato aggiuntivo che desideri raccogliere.

![Area di lavoro dello schema](assets/getting-started/schema-structure.png)

>[!NOTE]\
>Una volta salvati, gli schemi consentono solo *modifiche aggiuntive*. Per ulteriori informazioni, consulta [evoluzione schema](/help/xdm/schema/composition.md#evolution).

## Creare un flusso di dati {#datastream}

Un [Datastream](/help/datastreams/overview.md) è una configurazione che indica all&#39;Edge Network come gestire i dati inviati. Quando configuri un flusso di dati per inviare dati a un determinato prodotto, il flusso di dati trasmette automaticamente i dati rilevanti a ciascun prodotto in modo comprensibile per il prodotto specifico.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Seleziona **[!UICONTROL New datastream]**.
1. Assegnare allo stream di dati un nome desiderato e selezionare lo schema creato di recente in **[!UICONTROL Mapping schema]**.
1. Seleziona **[!UICONTROL Save]**.

![Elenco flussi di dati](assets/getting-started/datastreams.png)

## Creare una proprietà tag

Dopo aver creato uno schema e un flusso di dati, puoi creare e configurare una proprietà tag.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona **[!UICONTROL New property]**.
1. Assegna alla proprietà tag il nome e il dominio desiderati, quindi seleziona **[!UICONTROL Save]**.

## Installare l’estensione tag

L&#39;estensione tag Web SDK viene installata in una determinata proprietà tag.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**.
1. Seleziona la scheda **[!UICONTROL Catalog]**.
1. Utilizzare la ricerca per individuare l&#39;estensione **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Seleziona la scheda dell&#39;estensione, quindi fai clic su **[!UICONTROL Install]** a destra.

![Installa SDK](assets/getting-started/install-sdk.png)

## Configurare l’estensione tag

Quando si installa l&#39;estensione tag Web SDK, viene automaticamente visualizzata la pagina [Configurazione](configure/config-overview.md).

1. Nella [sezione Datastreams](configure/datastreams.md), seleziona lo stream di dati desiderato per ogni ambiente.

Tutte le altre impostazioni di configurazione vengono compilate automaticamente o sono facoltative. Impostare le impostazioni di configurazione desiderate, quindi selezionare **[!UICONTROL Save]**.

## Creare un elemento dati variabile

Adobe consiglia di utilizzare gli elementi dati [Variable](data-element-types.md#variable) per memorizzare il payload da inviare ad Adobe. Anche gli oggetti XDM sono elementi di dati disponibili, ma sono più vecchi e più limitati nei casi di utilizzo applicabili.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Selezionare **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**.
1. Assegna all&#39;elemento dati le seguenti proprietà a sinistra:
   * **[!UICONTROL Name]**: qualsiasi nome desiderato
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. Imposta le seguenti proprietà a destra:
   **Tipo di variabile**: XDM
   **[!UICONTROL Sandbox]**: la sandbox in cui hai creato lo schema
   **[!UICONTROL Schema]**: lo schema desiderato
1. Seleziona **[!UICONTROL Save]**.

## Creare una regola

Le regole determinano quando attivare qualcosa o impostare variabili. La creazione di una regola che viene eseguita ogni volta che viene caricata la libreria consente di popolare facilmente le variabili che desideri contengano un valore su ogni pagina.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Selezionare **[!UICONTROL Rules]** > **[!UICONTROL Add rule]**.
1. Assegna alla regola un nome desiderato.
1. Selezionare l&#39;icona &#39;`+`&#39; accanto a **[!UICONTROL Events]**.
1. Attribuisci all’evento le seguenti impostazioni:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. Seleziona **[!UICONTROL Keep changes]**.

I passaggi precedenti stabiliscono la parte dei criteri della regola, che viene attivata una volta caricata la libreria. Le seguenti misure stabiliscono l’azione da intraprendere quando tale criterio è soddisfatto.

1. Selezionare l&#39;icona &#39;`+`&#39; accanto a **[!UICONTROL Actions]**.
1. Assegna all’azione le seguenti impostazioni a sinistra:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. Imposta i seguenti campi a destra:
   * **[!UICONTROL XDM]**: elemento dati della variabile XDM
1. Seleziona **[!UICONTROL Keep changes]**.

![Configurazione azione](assets/getting-started/action-config.png)

## Pubblicazione

La proprietà tag contiene tutti i componenti necessari per inviare dati ad Edge Network.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Seleziona **[!UICONTROL Add library]**.
1. Assegna alla libreria un nome desiderato. Considerare questo nome simile al nome di un commit quando si utilizza il software di controllo delle versioni.
1. Impostare il menu a discesa dell&#39;ambiente su **[!UICONTROL Development]**.
1. Seleziona **[!UICONTROL Add all changed resources]**.
1. Seleziona **[!UICONTROL Save & build to Development]**.

Le modifiche ora vengono implementate nell&#39;ambiente di sviluppo.

1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Seleziona l’icona Installa accanto all’ambiente di sviluppo.
1. Installa il codice da incorporare in una pagina web di prova sul sito.

Dopo aver verificato che il tag funziona nell&#39;ambiente di sviluppo, è possibile utilizzare l&#39;interfaccia [!UICONTROL Publishing flow] per pubblicare la libreria nell&#39;ambiente di staging e infine in produzione.

1. Aggiungi l&#39;estensione e la regola a una **Libreria**, generala in un **Ambiente** e installa il codice di incorporamento sul tuo sito.
2. Convalida con **Adobe Experience Platform Debugger**.

Ora disponi di una configurazione snella che acquisisce gli eventi e li invia ad Edge Network. Ora puoi rafforzare ulteriormente l’implementazione aggiungendo campi allo schema, prodotti a un flusso di dati o elementi di dati alla proprietà tag.
