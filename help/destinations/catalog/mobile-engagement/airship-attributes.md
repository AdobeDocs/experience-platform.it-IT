---
keywords: attributi dirigibile;destinazione dirigibile
title: Connessione attributi dirigibili
description: Trasmettere facilmente i dati del pubblico Adobe a Airship come attributi del pubblico per il targeting all'interno di Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 2%

---

# Connessione [!DNL Airship Attributes] {#airship-attributes-destination}

## Panoramica {#overview}

[!DNL Airship] è la principale piattaforma di Customer Engagement e ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del profilo di Adobe in [!DNL Airship] come [Attributi](https://docs.airship.com/guides/audience/attributes/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni su [!DNL Airship], consulta i [documenti dirigibili](https://docs.airship.com).

>[!TIP]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Airship]. Per eventuali richieste di informazioni o richieste di aggiornamento, contattaci direttamente all&#39;indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti {#prerequisites}

Prima di poter inviare i tipi di pubblico a [!DNL Airship], è necessario:

* Abilitare gli attributi nel progetto [!DNL Airship].
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
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura dei campi. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Abilita attributi {#enable-attributes}

Gli attributi del profilo di Adobe Experience Platform sono simili agli attributi [!DNL Airship] e possono essere facilmente mappati gli uni agli altri in Platform utilizzando lo strumento di mappatura illustrato di seguito in questa pagina.

[!DNL Airship] progetti hanno diversi attributi predefiniti e predefiniti. Se hai un attributo personalizzato, devi prima definirlo in [!DNL Airship]. Per ulteriori informazioni, vedere [Configurazione e gestione degli attributi](https://docs.airship.com/tutorials/audience/attributes/).

## Genera token Bearer {#bearer-token}

Vai a **[!UICONTROL Impostazioni]**&quot; **[!UICONTROL API e integrazioni]** nel [Dashboard per dirigibili](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu a sinistra.

Fai clic su **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione attributi Adobi&quot;, e seleziona &quot;Tutti gli accessi&quot; per il ruolo.

Fai clic su **[!UICONTROL Crea token]** e salva i dettagli come riservati.

## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione [!DNL Airship Attributes], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Sfrutta i dati di profilo raccolti in Adobe Experience Platform per la personalizzazione del messaggio e contenuti avanzati in qualsiasi canale di [!DNL Airship]. Ad esempio, sfrutta i dati del profilo [!DNL Experience Platform] per impostare gli attributi di posizione in [!DNL Airship]. In questo modo, un marchio di hotel potrà visualizzare per ogni utente un&#39;immagine che indica la posizione più vicina all&#39;hotel.

### #2 del caso d’uso

Sfrutta gli attributi di Adobe Experience Platform per arricchire ulteriormente i profili [!DNL Airship] e combinarli con l&#39;SDK o con i dati predittivi [!DNL Airship]. Ad esempio, un rivenditore può creare un pubblico con lo stato di fedeltà e i dati sulla posizione (attributi da Platform) e [!DNL Airship] prevede di abbandonarli per inviare messaggi altamente mirati agli utenti con lo stato di fedeltà all&#39;oro che vivono a Las Vegas, NV, e hanno un&#39;alta probabilità di abbandono.

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
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Considerazioni sulla mappatura {#mapping-considerations}

Gli attributi [!DNL Airship] possono essere impostati su un canale, che rappresenta un&#39;istanza del dispositivo, ad esempio iPhone, oppure su un utente con nome, che mappa tutti i dispositivi di un utente su un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, seleziona il campo e-mail in **[!UICONTROL Attributi Source]** e mappali all&#39;utente denominato [!DNL Airship] nella colonna di destra in **[!UICONTROL Identità Target]**, come illustrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship/mapping.png)

Per gli identificatori che devono essere mappati su un canale, ovvero un dispositivo, mappa sul canale appropriato in base alla sorgente. Le immagini seguenti mostrano come vengono create due mappature:

* ID Advertising IDFA iOS in un canale iOS [!DNL Airship]
* Attributo Adobe `fullName` all&#39;attributo &quot;Full Name&quot; di [!DNL Airship]

>[!NOTE]
>
>Utilizza il nome descrittivo visualizzato nel dashboard [!DNL Airship] quando selezioni il campo di destinazione per la mappatura degli attributi.

**Identità mappa**

Seleziona campo di origine:

![Connetti agli attributi del dirigibile](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Seleziona campo di destinazione:

![Connetti agli attributi del dirigibile](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Attributo mappa**

Seleziona attributo di origine:

![Seleziona campo di origine](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Seleziona attributo di destinazione:

![Seleziona campo di destinazione](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verifica mappatura:

![Mappatura canale](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
