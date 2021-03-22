---
keywords: attributi del volo;destinazione del volo
title: Collegamento Attributi del volo
description: Trasmetti facilmente i dati di pubblico Adobe a Airship come Attributi di pubblico per il targeting all’interno di Airship.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 1%

---


# (Beta) [!DNL Airship Attributes] connessione {#airship-attributes-destination}

>[!IMPORTANT]
>
>La destinazione [!DNL Airship Attributes] in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

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

## Abilita gli attributi {#enable-attributes}

Gli attributi di profilo Adobe Experience Platform sono simili agli attributi [!DNL Airship] e possono essere facilmente mappati l’uno sull’altro in Platform utilizzando lo strumento di mappatura illustrato di seguito in questa pagina.

[!DNL Airship] i progetti dispongono di diversi attributi predefiniti e predefiniti. Se disponi di un attributo personalizzato, devi prima definirlo in [!DNL Airship]. Per ulteriori informazioni, consulta [Configurazione e gestione attributi](https://docs.airship.com/tutorials/audience/attributes/) .

## Genera token portatore {#bearer-token}

Vai a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** nel [Dashboard di bordo](https://go.airship.com) e seleziona **[!UICONTROL Tokens]** nel menu a sinistra.

Fai clic su **[!UICONTROL Create Token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione attributi Adobe&quot;, e seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Create Token]** e salva i dettagli come riservati.

## Casi d’uso {#use-cases}

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Airship Attributes], di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Sfrutta i dati di profilo raccolti in Adobe Experience Platform per la personalizzazione del messaggio e dei contenuti avanzati all’interno di uno qualsiasi dei canali di [!DNL Airship]. Ad esempio, sfrutta i dati di profilo [!DNL Experience Platform] per impostare gli attributi di posizione all’interno di [!DNL Airship]. In questo modo, un marchio dell&#39;hotel potrà mostrare un&#39;immagine della posizione più vicina per ogni utente.

### Caso d&#39;uso n. 2

Utilizza gli attributi di Adobe Experience Platform per arricchire ulteriormente i profili [!DNL Airship] e combinarli con i dati SDK o [!DNL Airship] predittivi. Ad esempio, un rivenditore può creare un segmento con stato di fedeltà e dati di posizione (attributi da Platform) e [!DNL Airship] previsti per l’abbandono dei dati per inviare messaggi altamente mirati agli utenti con stato di fidelizzazione dell’oro che vivono a Las Vegas, NV, e con un’elevata probabilità di esecuzione.

## Connetti a [!DNL Airship Attributes] {#connect-airship-attributes}

In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorri fino alla categoria **[!UICONTROL Mobile Engagement]** . Selezionare **[!DNL Airship Attributes]**, quindi selezionare **[!UICONTROL Configure]**.

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

![Connetti agli attributi del volo](../../assets/catalog/mobile-engagement/airship/catalog.png)

Nel passaggio **Account**, se in precedenza hai impostato una connessione alla destinazione [!DNL Airship Attributes], seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione a [!DNL Airship Attributes]. Seleziona **[!UICONTROL Connect to destination]** per collegare Adobe Experience Platform al progetto [!DNL Airship] utilizzando il token portatore generato dal dashboard [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali errate nel tuo account [!DNL Airship]. In questo modo non completa il flusso di lavoro con credenziali errate.

![Connetti agli attributi del volo](../../assets/catalog/mobile-engagement/airship/connect.png)

Una volta confermate le credenziali e quando Adobe Experience Platform è connesso al progetto [!DNL Airship], puoi selezionare **[!UICONTROL Next]** per procedere al passaggio **[!UICONTROL Setup]**.

Nel passaggio **[!UICONTROL Authentication]** immetti un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione.

Anche in questo passaggio, è possibile selezionare un centro dati US o EU, a seconda di quale [!DNL Airship] centro dati si applica a questa destinazione. Infine, seleziona uno o più **[!UICONTROL Marketing Actions]** per i quali verranno esportati i dati nella destinazione. Puoi scegliere tra le azioni di marketing definite da Adobe o crearne una tua. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Seleziona **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

![Connetti agli attributi del volo](../../assets/catalog/mobile-engagement/airship/select-domain.png)

La destinazione viene ora creata. Puoi selezionare **[!UICONTROL Save & Exit]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attivare i segmenti](#activate-segments) per il resto del flusso di lavoro.

## Attiva segmenti {#activate-segments}

Per attivare i segmenti su [!DNL Airship Attributes], segui i passaggi seguenti:

In **[!UICONTROL Destinations > Browse]**, seleziona la destinazione [!DNL Airship Attributes] in cui desideri attivare i segmenti.

![flusso di attivazione](../../assets/catalog/mobile-engagement/airship/browse.png)

Fare clic sul nome della destinazione. Viene visualizzato il flusso Attiva .

Se esiste già un flusso di attivazione per una destinazione, puoi vedere i segmenti attualmente inviati alla destinazione. Seleziona **[!UICONTROL Edit activation]** nella barra a destra e segui i passaggi riportati di seguito per modificare i dettagli di attivazione.

![flusso di attivazione](../../assets/catalog/mobile-engagement/airship/activate.png)

Seleziona **[!UICONTROL Activate]**. Nel flusso di lavoro **[!UICONTROL Activate destination]**, nella pagina **[!UICONTROL Select Segments]** seleziona i segmenti da inviare a [!DNL Airship Attributes].

![da segmenti a destinazione](../../assets/catalog/mobile-engagement/airship/select-segments.png)

Nel passaggio **[!UICONTROL Mapping]** , seleziona gli attributi e le identità dallo schema [XDM](../../../xdm/home.md) da mappare allo schema di destinazione. Seleziona **[!UICONTROL Add new mapping]** per sfogliare lo schema e mapparlo sull&#39;identità di destinazione corrispondente.

![schermata iniziale della mappatura identità](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] Gli attributi possono essere impostati su un canale, che rappresenta un&#39;istanza del dispositivo, ad esempio iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente a un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail in testo normale (con hash) come identità principale, seleziona il campo e-mail nel **[!UICONTROL Source Attributes]** e mappalo sull’ [!DNL Airship] utente denominato nella colonna di destra sotto **[!UICONTROL Target Identities]**, come mostrato di seguito.

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

Nella pagina **[!UICONTROL Segment schedule]** la pianificazione è attualmente disabilitata. Fai clic su **[!UICONTROL Next]** per continuare il passaggio di revisione.

![Pianificazione disabilitata](../../assets/catalog/mobile-engagement/airship/scheduling.png)

Nella pagina **[!UICONTROL Review]** è disponibile un riepilogo della selezione. Seleziona **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** per modificare le impostazioni oppure **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione dei criteri](../../../data-governance/enforcement/auto-enforcement.md) nella sezione relativa alla governance dei dati .

![confirm-selection](../../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, seleziona **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![revisione](../../assets/catalog/mobile-engagement/airship/review.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [Panoramica sulla governance dei dati](../../../data-governance/home.md).
