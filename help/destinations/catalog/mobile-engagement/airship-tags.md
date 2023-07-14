---
keywords: etichetta dirigibile;destinazione dirigibile
title: Connessione tag dirigibili
description: Trasmetti facilmente i dati del pubblico Adobe a Airship come tag del pubblico per il targeting all’interno di Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# [!DNL Airship Tags] connessione {#airship-tags-destination}

## Panoramica

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del pubblico di Adobe Experience Platform in [!DNL Airship] as [Tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l’attivazione.

Per ulteriori informazioni su [!DNL Airship], vedere [Documenti dirigibili](https://docs.airship.com).


>[!TIP]
>
>Questa pagina della documentazione è stata creata da [!DNL Airship] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattale direttamente all’indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti

Prima di poter inviare il pubblico Adobe Experience Platform a [!DNL Airship], è necessario:

* Creare un gruppo di tag nel [!DNL Airship] progetto.
* Genera un token Bearer per l’autenticazione.

>[!TIP]
> 
>Creare un [!DNL Airship] account tramite [questo collegamento di abbonamento](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Supporto di tipi di pubblico esterni {#external-audiences-support}

Tutte le destinazioni supportano l’attivazione dei tipi di pubblico generati tramite l’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md).

Inoltre, questa destinazione supporta anche l’attivazione dei tipi di pubblico esterni descritti nella tabella seguente.

| Tipo di pubblico esterno | Descrizione |
---------|----------|
| Caricamenti personalizzati | Tipi di pubblico acquisiti in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori utilizzati nella destinazione Tag dirigibili. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Gruppi di tag

Il concetto di pubblico in Adobe Experience Platform è simile a [Tag](https://docs.airship.com/guides/audience/tags/) in dirigibili, con lievi differenze di attuazione. Questa integrazione mappa lo stato di un utente di [appartenenza a un segmento di Experience Platform](../../../xdm/field-groups/profile/segmentation.md) alla presenza o meno di un [!DNL Airship] tag. Ad esempio, in un pubblico di Platform in cui `xdm:status` modifiche apportate a `realized`, il tag viene aggiunto al [!DNL Airship] channel or named user a cui è mappato questo profilo. Se il `xdm:status` modifiche apportate a `exited`, il tag viene rimosso.

Per abilitare questa integrazione, crea un’ *gruppo di tag* in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Durante la creazione di un nuovo gruppo di tag **Non controllare** il pulsante di opzione che indica &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l’integrazione dei tag di Adobe avrà esito negativo.

Consulta [Gestione gruppi di tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) per istruzioni sulla creazione del gruppo di tag.

## Genera token Bearer

Vai a **[!UICONTROL Impostazioni]** &quot; **[!UICONTROL API e integrazioni]** nel [Cruscotto del dirigibile](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu di sinistra.

Clic **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione tag Adobe&quot;, e seleziona &quot;Accesso completo&quot; per il ruolo.

Clic **[!UICONTROL Crea token]** e salva i dettagli come confidenziali.

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Airship Tags] destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

I rivenditori o le piattaforme di intrattenimento possono creare profili di utenti sui loro clienti fidelizzati e trasmettere tali tipi di pubblico a [!DNL Airship] per il targeting dei messaggi nelle campagne per dispositivi mobili.

### #2 del caso d’uso

Attivare messaggi uno-a-uno in tempo reale quando gli utenti entrano o escono da un pubblico specifico all’interno di Adobe Experience Platform.

Ad esempio, un rivenditore imposta in Platform un pubblico specifico per il brand dei jeans. Il rivenditore può attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans a una marca specifica.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL Token Bearer]**: il token Bearer generato da [!DNL Airship] dashboard.

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: inserisci un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: inserisci una descrizione per questa destinazione.
* **[!UICONTROL Dominio]**: seleziona un centro dati statunitense o dell’UE, a seconda di quale [!DNL Airship] data center applicabile a questa destinazione.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Considerazioni sulla mappatura {#mapping-considerations}

[!DNL Airship] i tag possono essere impostati su un canale, che rappresenta un’istanza del dispositivo, ad esempio iPhone, oppure su un utente con nome, che mappa tutti i dispositivi di un utente su un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, seleziona il campo e-mail nel tuo **[!UICONTROL Attributi sorgente]** e mappare su [!DNL Airship] utente con nome nella colonna di destra in **[!UICONTROL Identità di destinazione]**, come illustrato di seguito.

![Mappatura utente denominato](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Per gli identificatori che devono essere mappati su un canale, ovvero un dispositivo, mappa sul canale appropriato in base alla sorgente. Le immagini seguenti mostrano come mappare un Google Advertising ID su un [!DNL Airship] Canale Android.

![Connetti ai tag dirigibili](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Connetti ai tag dirigibili](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mappatura canale](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
