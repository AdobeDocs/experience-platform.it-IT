---
keywords: targhette di bordo;destinazione di volo
title: Collegamento dei tag dell'aeroporto
description: Trasmetti facilmente i dati di pubblico Adobe a Airship come tag di pubblico per il targeting all’interno di Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# [!DNL Airship Tags] connection {#airship-tags-destination}

## Panoramica

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del segmento Adobe Experience Platform a [!DNL Airship] come [Tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni [!DNL Airship], vedi [Documenti di volo](https://docs.airship.com).


>[!TIP]
>
>Questa pagina della documentazione è stata creata da [!DNL Airship] squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti

Prima di poter inviare i segmenti Adobe Experience Platform a [!DNL Airship], devi:

* Creare un gruppo di tag nel [!DNL Airship] progetto.
* Genera un token portatore per l’autenticazione.

>[!TIP]
> 
>Crea un [!DNL Airship] account tramite [questo link di registrazione](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori utilizzati nella destinazione Tag di bordo. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Gruppi di tag

Il concetto di segmenti in Adobe Experience Platform è simile a [Tag](https://docs.airship.com/guides/audience/tags/) in Airship, con lievi differenze di attuazione. Questa integrazione mappa lo stato di un utente [appartenenza a un segmento di Experience Platform](../../../xdm/field-groups/profile/segmentation.md) alla presenza o alla non presenza di un [!DNL Airship] tag . Ad esempio, in un segmento Platform in cui la `xdm:status` modifiche a `realized`, il tag viene aggiunto al [!DNL Airship] canale o utente con nome a cui è mappato questo profilo. Se la `xdm:status` modifiche a `exited`, il tag viene rimosso.

Per abilitare questa integrazione, crea un *gruppo di tag* in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Durante la creazione del nuovo gruppo di tag **Non controllare** il pulsante di scelta che dice &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l’integrazione dei tag di Adobe avrà esito negativo.

Vedi [Gestire i gruppi di tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) per istruzioni su come creare il gruppo di tag.

## Genera token portatore

Vai a **[!UICONTROL Impostazioni]** &quot; **[!UICONTROL API e integrazioni]** in [Dashboard di bordo](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu a sinistra.

Fai clic su **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione tag di Adobe&quot;, quindi seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Crea token]** e salva i dettagli come riservati.

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Airship Tags] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

I rivenditori o le piattaforme di intrattenimento possono creare profili utente sui loro clienti fidelizzati e trasmettere tali segmenti a [!DNL Airship] per il targeting dei messaggi sulle campagne mobile.

### Caso d&#39;uso n. 2

Attiva messaggi uno-a-uno in tempo reale quando gli utenti rientrano in o fuori segmenti specifici all’interno di Adobe Experience Platform.

Ad esempio, un rivenditore imposta un segmento specifico del marchio jeans in Platform. Il rivenditore può ora attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans su un marchio specifico.

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Token portatore]**: il token portatore generato da [!DNL Airship] dashboard.
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione per la destinazione.
* **[!UICONTROL Dominio]**: selezionare un centro dati USA o UE, a seconda di quale [!DNL Airship] data center si applica a questa destinazione.


## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Considerazioni sulla mappatura {#mapping-considerations}

[!DNL Airship] I tag possono essere impostati su un canale, che rappresenta l’istanza del dispositivo, ad esempio iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente a un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail in testo normale (senza hash) come identità principale, seleziona il campo e-mail nel **[!UICONTROL Attributi di origine]** e mappare [!DNL Airship] utente con nome nella colonna di destra sotto **[!UICONTROL Identità di destinazione]**, come illustrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Per gli identificatori che devono essere mappati su un canale, cioè un dispositivo, mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come mappare un Google Advertising ID su un [!DNL Airship] Canale Android.

![Connetti ai tag di volo](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Connetti ai tag di volo](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mappatura del canale](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
