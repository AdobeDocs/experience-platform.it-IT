---
keywords: attributi dirigibile;destinazione dirigibile
title: Connessione attributi dirigibili
description: Trasmettere facilmente i dati del pubblico Adobe a Airship come attributi del pubblico per il targeting all'interno di Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 2%

---

# [!DNL Airship Attributes] connessione {#airship-attributes-destination}

## Panoramica {#overview}

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del profilo di Adobe in [!DNL Airship] as [Attributi](https://docs.airship.com/guides/audience/attributes/) per il targeting o l’attivazione.

Per ulteriori informazioni su [!DNL Airship], vedere [Documenti dirigibili](https://docs.airship.com).

>[!TIP]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da [!DNL Airship] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti {#prerequisites}

Prima di poter inviare i tipi di pubblico a [!DNL Airship], è necessario:

* Abilitare gli attributi nel [!DNL Airship] progetto.
* Genera un token Bearer per l’autenticazione.

>[!TIP]
>
>Creare un [!DNL Airship] account tramite [questo collegamento di abbonamento](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura dei campi. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Abilita attributi {#enable-attributes}

Gli attributi del profilo Adobe Experience Platform sono simili a [!DNL Airship] e possono essere facilmente mappati l’uno sull’altro in Platform utilizzando lo strumento di mappatura illustrato più avanti in questa pagina.

[!DNL Airship] i progetti hanno diversi attributi predefiniti e predefiniti. Se disponi di un attributo personalizzato, devi definirlo in [!DNL Airship] prima. Consulta [Impostazione e gestione degli attributi](https://docs.airship.com/tutorials/audience/attributes/) per i dettagli.

## Genera token Bearer {#bearer-token}

Vai a **[!UICONTROL Impostazioni]** &quot; **[!UICONTROL API e integrazioni]** nel [Cruscotto del dirigibile](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu di sinistra.

Clic **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione attributi Adobi&quot;, e seleziona &quot;Tutti gli accessi&quot; per il ruolo.

Clic **[!UICONTROL Crea token]** e salva i dettagli come confidenziali.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Airship Attributes] destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Sfrutta i dati di profilo raccolti in Adobe Experience Platform per la personalizzazione del messaggio e contenuti avanzati in qualsiasi [!DNL Airship]canali di. Ad esempio, sfruttare [!DNL Experience Platform] dati di profilo per impostare gli attributi di posizione in [!DNL Airship]. In questo modo, un marchio di hotel potrà visualizzare per ogni utente un&#39;immagine che indica la posizione più vicina all&#39;hotel.

### #2 del caso d’uso

Sfruttare gli attributi di Adobe Experience Platform per arricchire ulteriormente [!DNL Airship] e combinarli con l’SDK o [!DNL Airship] dati predittivi. Ad esempio, un rivenditore può creare un pubblico con lo stato di fedeltà e i dati sulla posizione (attributi da Platform) e [!DNL Airship] si prevede che abbandoneranno i dati per inviare messaggi altamente mirati agli utenti con status di fidelizzazione all’oro che vivono a Las Vegas, NV, e hanno un’alta probabilità di abbandono.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL Token Bearer]**: il token Bearer generato da [!DNL Airship] dashboard.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: inserisci un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: inserisci una descrizione per questa destinazione.
* **[!UICONTROL Dominio]**: seleziona un centro dati statunitense o dell’UE, a seconda di quale [!DNL Airship] data center applicabile a questa destinazione.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Considerazioni sulla mappatura {#mapping-considerations}

[!DNL Airship] gli attributi possono essere impostati su un canale, che rappresenta un’istanza del dispositivo, ad esempio iPhone, oppure su un utente con nome, che mappa tutti i dispositivi di un utente su un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, seleziona il campo e-mail nel tuo **[!UICONTROL Attributi sorgente]** e mappare su [!DNL Airship] utente con nome nella colonna di destra in **[!UICONTROL Identità di destinazione]**, come illustrato di seguito.

![Mappatura utente denominato](../../assets/catalog/mobile-engagement/airship/mapping.png)

Per gli identificatori che devono essere mappati su un canale, ovvero un dispositivo, mappa sul canale appropriato in base alla sorgente. Le immagini seguenti mostrano come vengono create due mappature:

* IDFA iOS Advertising ID per un [!DNL Airship] Canale iOS
* Adobe `fullName` attribuire a [!DNL Airship] Attributo &quot;Nome completo&quot;

>[!NOTE]
>
>Utilizza il nome descrittivo visualizzato in [!DNL Airship] quando si seleziona il campo di destinazione per la mappatura degli attributi.

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

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](../../../data-governance/home.md).
