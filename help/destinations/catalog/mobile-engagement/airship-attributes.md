---
keywords: attributi del volo;destinazione del volo
title: Collegamento Attributi del volo
description: Trasmetti facilmente i dati di pubblico Adobe a Airship come Attributi di pubblico per il targeting all’interno di Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Airship Attributes] connection {#airship-attributes-destination}

## Panoramica {#overview}

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del profilo di Adobe a [!DNL Airship] come [Attributi](https://docs.airship.com/guides/audience/attributes/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni [!DNL Airship], vedi [Documenti di volo](https://docs.airship.com).

>[!TIP]
>
>Questa pagina della documentazione è stata creata da [!DNL Airship] squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti {#prerequisites}

Prima di inviare i segmenti di pubblico a [!DNL Airship], devi:

* Abilitare gli attributi nel [!DNL Airship] progetto.
* Genera un token portatore per l’autenticazione.

>[!TIP]
>
>Crea un [!DNL Airship] account tramite [questo link di registrazione](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura del campo. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Abilitare gli attributi {#enable-attributes}

Gli attributi di profilo Adobe Experience Platform sono simili a [!DNL Airship] e può essere facilmente mappato l’uno sull’altro in Platform utilizzando lo strumento di mappatura illustrato più avanti in questa pagina.

[!DNL Airship] i progetti dispongono di diversi attributi predefiniti e predefiniti. Se disponi di un attributo personalizzato, devi definirlo in [!DNL Airship] prima. Vedi [Impostare e gestire gli attributi](https://docs.airship.com/tutorials/audience/attributes/) per i dettagli.

## Genera token portatore {#bearer-token}

Vai a **[!UICONTROL Impostazioni]** &quot; **[!UICONTROL API e integrazioni]** in [Dashboard di bordo](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu a sinistra.

Fai clic su **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione attributi Adobe&quot;, e seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Crea token]** e salva i dettagli come riservati.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Airship Attributes] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Sfrutta i dati di profilo raccolti in Adobe Experience Platform per la personalizzazione del messaggio e dei contenuti avanzati all’interno di uno dei [!DNL Airship]I canali. Ad esempio, la leva finanziaria [!DNL Experience Platform] dati di profilo per impostare gli attributi di posizione all’interno di [!DNL Airship]. In questo modo, un marchio dell&#39;hotel potrà mostrare un&#39;immagine della posizione più vicina per ogni utente.

### Caso d&#39;uso n. 2

Utilizzo degli attributi da Adobe Experience Platform per arricchire ulteriormente [!DNL Airship] Profili e combinali con SDK o [!DNL Airship] dati predittivi. Ad esempio, un rivenditore può creare un segmento con lo stato fedeltà e i dati di posizione (attributi da Platform) e [!DNL Airship] prevedevano di inviare dati altamente mirati agli utenti in stato di fidelizzazione dell&#39;oro che vivono a Las Vegas, NV, e hanno un&#39;alta probabilità di fiorire.

## Collegati alla destinazione {#connect}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Token portatore]**: il token portatore generato da [!DNL Airship] dashboard.
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione per la destinazione.
* **[!UICONTROL Dominio]**: selezionare un centro dati USA o UE, a seconda di quale [!DNL Airship] data center si applica a questa destinazione.

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Considerazioni sulla mappatura {#mapping-considerations}

[!DNL Airship] Gli attributi possono essere impostati su un canale, che rappresenta l&#39;istanza del dispositivo, ad esempio iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente a un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail in testo normale (senza hash) come identità principale, seleziona il campo e-mail nel **[!UICONTROL Attributi di origine]** e mappare [!DNL Airship] utente con nome nella colonna di destra sotto **[!UICONTROL Identità di destinazione]**, come illustrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship/mapping.png)

Per gli identificatori che devono essere mappati su un canale, cioè un dispositivo, mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come vengono create due mappature:

* IDFA iOS Advertising ID a un [!DNL Airship] Canale iOS
* Adobe `fullName` attributo a [!DNL Airship] Attributo &quot;Full Name&quot;

>[!NOTE]
>
>Utilizza il nome descrittivo visualizzato nella [!DNL Airship] dashboard quando selezioni il campo di destinazione per la mappatura degli attributi.

**Mappa identità**

Selezionare il campo di origine:

![Connetti agli attributi del volo](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Seleziona il campo di destinazione:

![Connetti agli attributi del volo](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Attributo mappa**

Seleziona attributo di origine:

![Selezionare il campo di origine](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Seleziona l&#39;attributo di destinazione:

![Selezionare il campo di destinazione](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verifica mappatura:

![Mappatura del canale](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
