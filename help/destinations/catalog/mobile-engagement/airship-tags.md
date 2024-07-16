---
keywords: etichetta dirigibile;destinazione dirigibile
title: Connessione tag dirigibili
description: Trasmetti facilmente i dati del pubblico Adobe a Airship come tag del pubblico per il targeting all’interno di Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 2%

---

# Connessione [!DNL Airship Tags] {#airship-tags-destination}

## Panoramica

[!DNL Airship] è la principale piattaforma di Customer Engagement e ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del pubblico di Adobe Experience Platform in [!DNL Airship] come [Tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni su [!DNL Airship], consulta i [documenti dirigibili](https://docs.airship.com).


>[!TIP]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Airship]. Per eventuali richieste di informazioni o richieste di aggiornamento, contattaci direttamente all&#39;indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti

Prima di poter inviare i tipi di pubblico di Adobe Experience Platform a [!DNL Airship], è necessario:

* Crea un gruppo di tag nel progetto [!DNL Airship].
* Genera un token Bearer per l’autenticazione.

>[!TIP]
> 
>Se non lo hai già fatto, crea un account [!DNL Airship] tramite [questo collegamento per la registrazione](https://go.airship.eu/accounts/register/plan/starter/).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori utilizzati nella destinazione Tag dirigibili. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Gruppi di tag

Il concetto di pubblico in Adobe Experience Platform è simile a [Tag](https://docs.airship.com/guides/audience/tags/) in Airship, con lievi differenze nell&#39;implementazione. Questa integrazione mappa lo stato dell&#39;appartenenza [di un utente in un segmento di Experience Platform](../../../xdm/field-groups/profile/segmentation.md) alla presenza o meno di un tag [!DNL Airship]. Ad esempio, in un pubblico di Platform in cui `xdm:status` diventa `realized`, il tag viene aggiunto al canale [!DNL Airship] o all&#39;utente con nome a cui è mappato questo profilo. Se `xdm:status` diventa `exited`, il tag viene rimosso.

Per abilitare questa integrazione, creare un *gruppo di tag* in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Durante la creazione del nuovo gruppo di tag **Non selezionare** il pulsante di opzione &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l’integrazione dei tag di Adobe avrà esito negativo.

Per istruzioni sulla creazione del gruppo di tag, consulta [Gestisci gruppi di tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups).

## Genera token Bearer

Vai a **[!UICONTROL Impostazioni]**&quot; **[!UICONTROL API e integrazioni]** nel [Dashboard per dirigibili](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu a sinistra.

Fai clic su **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione tag Adobe&quot;, e seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Crea token]** e salva i dettagli come riservati.

## Casi d’uso

Per capire meglio come e quando utilizzare la destinazione [!DNL Airship Tags], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

I rivenditori o le piattaforme di intrattenimento possono creare profili utente sui propri clienti fidelizzati e passare tali tipi di pubblico in [!DNL Airship] per il targeting dei messaggi nelle campagne mobili.

### #2 del caso d’uso

Attivare messaggi uno-a-uno in tempo reale quando gli utenti entrano o escono da un pubblico specifico all’interno di Adobe Experience Platform.

Ad esempio, un rivenditore imposta in Platform un pubblico specifico per il brand dei jeans. Il rivenditore può attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans a una marca specifica.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL Token Bearer]**: il token Bearer generato dal dashboard [!DNL Airship].

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immettere un nome che consenta di identificare la destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione per questa destinazione.
* **[!UICONTROL Dominio]**: selezionare un data center statunitense o dell&#39;UE, a seconda del data center [!DNL Airship] applicabile a questa destinazione.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Considerazioni sulla mappatura {#mapping-considerations}

I tag [!DNL Airship] possono essere impostati su un canale, che rappresenta un&#39;istanza del dispositivo, ad esempio iPhone, oppure su un utente con nome, che mappa tutti i dispositivi di un utente su un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, seleziona il campo e-mail in **[!UICONTROL Attributi Source]** e mappali all&#39;utente denominato [!DNL Airship] nella colonna di destra in **[!UICONTROL Identità Target]**, come illustrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Per gli identificatori che devono essere mappati su un canale, ovvero un dispositivo, mappa sul canale appropriato in base alla sorgente. Nelle immagini seguenti viene illustrato come mappare un Advertising ID di Google a un canale Android [!DNL Airship].

![Connetti ai tag per dirigibili](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Connetti ai tag dirigibili](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mappatura canale](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
