---
keywords: targhette di bordo;destinazione di volo
title: Collegamento dei tag dell'aeroporto
description: Trasmetti facilmente i dati di pubblico Adobe a Airship come tag di pubblico per il targeting all’interno di Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# [!DNL Airship Tags] connection {#airship-tags-destination}

## Panoramica

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del segmento Adobe Experience Platform in [!DNL Airship] come [Tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l’attivazione.

Per ulteriori informazioni su [!DNL Airship], consulta le [Documenti di navigazione aerea](https://docs.airship.com).


>[!TIP]
>
>Questa pagina della documentazione è stata creata dal team [!DNL Airship]. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente su [support.airship.com](https://support.airship.com/).

## Prerequisiti

Prima di inviare i segmenti Adobe Experience Platform a [!DNL Airship], devi:

* Crea un gruppo di tag nel progetto [!DNL Airship] .
* Genera un token portatore per l’autenticazione.

>[!TIP]
> 
>Crea un account [!DNL Airship] tramite [questo collegamento di registrazione](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Gruppi di tag

Il concetto di segmenti in Adobe Experience Platform è simile a [Tag](https://docs.airship.com/guides/audience/tags/) in Airship, con lievi differenze nell’implementazione. Questa integrazione mappa lo stato dell’ [appartenenza di un utente in un segmento di Experience Platform](../../../xdm/field-groups/profile/segmentation.md) alla presenza o alla non presenza di un tag [!DNL Airship]. Ad esempio, in un segmento di Platform in cui `xdm:status` cambia in `realized`, il tag viene aggiunto al canale [!DNL Airship] o all’utente con nome a cui è mappato questo profilo. Se il tag `xdm:status` diventa `exited`, viene rimosso.

Per abilitare questa integrazione, crea un *gruppo di tag* in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Durante la creazione del nuovo gruppo di tag **Non selezionare** il pulsante di scelta &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l’integrazione dei tag di Adobe avrà esito negativo.

Per istruzioni sulla creazione del gruppo di tag, consulta [Gestione gruppi di tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) .

## Genera token portatore

Vai a **[!UICONTROL Impostazioni]**&quot; **[!UICONTROL API e integrazioni]** nel [Dashboard di navigazione](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu a sinistra.

Fai clic su **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione tag di Adobe&quot;, quindi seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Crea token]** e salva i dettagli come riservati.

## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Airship Tags], di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

I rivenditori o le piattaforme di intrattenimento possono creare profili utente sui loro clienti fidelizzati e passare tali segmenti in [!DNL Airship] per il targeting dei messaggi sulle campagne mobili.

### Caso d&#39;uso n. 2

Attiva messaggi uno-a-uno in tempo reale quando gli utenti rientrano in o fuori segmenti specifici all’interno di Adobe Experience Platform.

Ad esempio, un rivenditore imposta un segmento specifico del marchio jeans in Platform. Il rivenditore può ora attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans su un marchio specifico.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Token]** portatore: token portatore generato dal  [!DNL Airship] dashboard.
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione per la destinazione.
* **[!UICONTROL Dominio]**: selezionare un centro dati USA o UE, a seconda del centro  [!DNL Airship] dati applicato a questa destinazione.


## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

## Considerazioni sulla mappatura {#mapping-considerations}

[!DNL Airship] I tag possono essere impostati su un canale, che rappresenta l’istanza del dispositivo, ad esempio l’iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente con un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail in testo normale (con hash) come identità principale, seleziona il campo e-mail in **[!UICONTROL Attributi di origine]** e mappalo sull’ [!DNL Airship] utente denominato nella colonna di destra in **[!UICONTROL Identità di destinazione]**, come mostrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Per gli identificatori che devono essere mappati su un canale, cioè un dispositivo, mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come mappare un Google Advertising ID su un canale [!DNL Airship] Android.

![Connetti a ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![TagsConnetti a ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![TagsMappatura canale](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta [Panoramica sulla governance dei dati](../../../data-governance/home.md).
