---
keywords: attributi del volo;destinazione del volo
title: Collegamento Attributi del volo
description: Trasmetti facilmente i dati di pubblico Adobe a Airship come Attributi di pubblico per il targeting all’interno di Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# (Beta) Connessione [!DNL Airship Attributes] {#airship-attributes-destination}

>[!IMPORTANT]
>
>La destinazione [!DNL Airship Attributes] in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del profilo di Adobe in [!DNL Airship] come [Attributi](https://docs.airship.com/guides/audience/attributes/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni su [!DNL Airship], consulta le [Documenti di navigazione aerea](https://docs.airship.com).

>[!TIP]
>
>Questa pagina della documentazione è stata creata dal team [!DNL Airship]. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente su [support.airship.com](https://support.airship.com/).

## Prerequisiti {#prerequisites}

Prima di inviare i segmenti di pubblico a [!DNL Airship], devi:

* Abilita gli attributi nel tuo progetto [!DNL Airship].
* Genera un token portatore per l’autenticazione.

>[!TIP]
>
>Crea un account [!DNL Airship] tramite [questo collegamento di registrazione](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Abilitare gli attributi {#enable-attributes}

Gli attributi di profilo Adobe Experience Platform sono simili agli attributi [!DNL Airship] e possono essere facilmente mappati l’uno sull’altro in Platform utilizzando lo strumento di mappatura illustrato di seguito in questa pagina.

[!DNL Airship] i progetti dispongono di diversi attributi predefiniti e predefiniti. Se disponi di un attributo personalizzato, devi prima definirlo in [!DNL Airship]. Per ulteriori informazioni, consulta [Configurazione e gestione attributi](https://docs.airship.com/tutorials/audience/attributes/) .

## Genera token portatore {#bearer-token}

Vai a **[!UICONTROL Impostazioni]**&quot; **[!UICONTROL API e integrazioni]** nel [Dashboard di navigazione](https://go.airship.com) e seleziona **[!UICONTROL Token]** nel menu a sinistra.

Fai clic su **[!UICONTROL Crea token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione attributi Adobe&quot;, e seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Crea token]** e salva i dettagli come riservati.

## Casi di utilizzo {#use-cases}

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Airship Attributes], di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Sfrutta i dati di profilo raccolti in Adobe Experience Platform per la personalizzazione del messaggio e dei contenuti avanzati all’interno di uno qualsiasi dei canali di [!DNL Airship]. Ad esempio, sfrutta i dati di profilo [!DNL Experience Platform] per impostare gli attributi di posizione all’interno di [!DNL Airship]. In questo modo, un marchio dell&#39;hotel potrà mostrare un&#39;immagine della posizione più vicina per ogni utente.

### Caso d&#39;uso n. 2

Utilizza gli attributi di Adobe Experience Platform per arricchire ulteriormente i profili [!DNL Airship] e combinarli con i dati SDK o [!DNL Airship] predittivi. Ad esempio, un rivenditore può creare un segmento con stato di fedeltà e dati di posizione (attributi da Platform) e [!DNL Airship] previsti per l’abbandono dei dati per inviare messaggi altamente mirati agli utenti con stato di fidelizzazione dell’oro che vivono a Las Vegas, NV, e con un’elevata probabilità di esecuzione.

## Collegati alla destinazione {#connect}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Token]** portatore: token portatore generato dal  [!DNL Airship] dashboard.
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione per la destinazione.
* **[!UICONTROL Dominio]**: selezionare un centro dati USA o UE, a seconda del centro  [!DNL Airship] dati applicato a questa destinazione.

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

## Considerazioni sulla mappatura {#mapping-considerations}

[!DNL Airship] Gli attributi possono essere impostati su un canale, che rappresenta un&#39;istanza del dispositivo, ad esempio iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente a un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail in testo normale (con hash) come identità principale, seleziona il campo e-mail in **[!UICONTROL Attributi di origine]** e mappalo sull’ [!DNL Airship] utente denominato nella colonna di destra in **[!UICONTROL Identità di destinazione]**, come mostrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship/mapping.png)

Per gli identificatori che devono essere mappati su un canale, cioè un dispositivo, mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come vengono create due mappature:

* IDFA iOS Advertising ID to an [!DNL Airship] iOS channel
* Adobe `fullName` attributo all&#39;attributo [!DNL Airship] &quot;Nome completo&quot;

>[!NOTE]
>
>Utilizza il nome descrittivo visualizzato nel dashboard [!DNL Airship] quando selezioni il campo di destinazione per la mappatura degli attributi.

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

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [Panoramica sulla governance dei dati](../../../data-governance/home.md).
