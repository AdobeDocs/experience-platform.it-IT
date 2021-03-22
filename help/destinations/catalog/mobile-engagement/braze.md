---
keywords: mobile; branco; messaggistica;
title: Collegamento del freno
description: Braze è una piattaforma completa di coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---


# (Beta) Connessione [!DNL Braze]

>[!IMPORTANT]
>
>La destinazione Braze in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

La destinazione [!DNL Braze] ti aiuta a inviare i dati del profilo a [!DNL Braze].

[!DNL Braze] è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.

Per inviare i dati del profilo a [!DNL Braze], è necessario prima connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Tieni presente i seguenti dettagli specifici della destinazione [!DNL Braze]:

* [!DNL Adobe Experience Platform] i segmenti vengono esportati in  [!DNL Braze] sotto l’ `AdobeExperiencePlatformSegments` attributo .

>[!NOTE]
>
>Tieni presente che l’invio di attributi personalizzati aggiuntivi a [!DNL Braze] può causare un aumento del consumo di [!DNL Braze] punti dati. Consulta il tuo account manager [!DNL Braze] prima di inviare attributi personalizzati aggiuntivi.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio indirizzare l’attività agli utenti in una destinazione di coinvolgimento mobile, con i segmenti generati in [!DNL Adobe Experience Platform]. Inoltre, voglio offrire loro esperienze personalizzate, basate sugli attributi dei loro profili [!DNL Adobe Experience Platform], non appena i segmenti e i profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| external_id | Identificatore [!DNL Braze] personalizzato che supporta la mappatura di qualsiasi identità. | Puoi inviare qualsiasi [identità](../../../identity-service/namespaces.md) alla destinazione [!DNL Braze], purché la mappi sul [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Tipo di esportazione {#export-type}

**[!DNL Profile-based]** - si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura del campo.
[!DNL Adobe Experience Platform] i segmenti vengono esportati in  [!DNL Braze] sotto l’ `AdobeExperiencePlatformSegments` attributo .

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Braze] e selezionare **[!UICONTROL Configure]**.

![Configurare la destinazione del freno](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.
>
>![Attiva destinazione del freno](../../assets/catalog/mobile-engagement/braze/activate.png)

Nel passaggio [!UICONTROL Account] , devi fornire il token dell’account [!DNL Braze] . Questa è la chiave [!DNL Braze] [!DNL API]. Puoi trovare istruzioni dettagliate su come ottenere la tua chiave [!DNL API] qui: [Panoramica della chiave API REST](https://www.braze.com/docs/api/api_key/). Immetti il token e fai clic su **[!UICONTROL Connect to destination]**.

![Fase dell&#39;account di destinazione del freno](../../assets/catalog/mobile-engagement/braze/account.png)

Fai clic su **[!UICONTROL Next]**. Nel passaggio [!UICONTROL Authentication] , è necessario inserire i dettagli di connessione [!DNL Braze]:
* **[!UICONTROL Name]**: immetti un nome in base al quale riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: inserisci una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Endpoint Instance]**: chiedi al tuo  [!DNL Braze] rappresentante quale istanza dell&#39;endpoint devi utilizzare.
* **[!UICONTROL Marketing action]**: le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Per informazioni sulle singole azioni di marketing definite da Adobe, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Passaggio di autenticazione del freno](../../assets/catalog/mobile-engagement/braze/authentication.png)

Fai clic su **[!UICONTROL Create destination]**. La destinazione viene ora creata. Puoi fare clic su **[!UICONTROL Save & Exit]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md#select-attributes) .

## Mappatura del campo {#field-mapping}

Per inviare correttamente i dati del pubblico da [!DNL Adobe Experience Platform] alla destinazione [!DNL Braze], devi passare attraverso il passaggio di mappatura dei campi .

La mappatura consiste nella creazione di un collegamento tra i campi dello schema [!DNL Experience Data Model] (XDM) nell&#39;account [!DNL Platform] e i corrispondenti equivalenti dalla destinazione di destinazione.

Per mappare correttamente i campi XDM sui campi di destinazione [!DNL Braze], effettua le seguenti operazioni:

Nel passaggio [!UICONTROL Mapping], fai clic su **[!UICONTROL Add new mapping]**.

![Mappatura aggiunta destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping.png)

Nella sezione [!UICONTROL Source Field] fare clic sul pulsante freccia accanto al campo vuoto.

![Mappatura della sorgente del freno](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Nella finestra [!UICONTROL Select source field], puoi scegliere tra due categorie di campi XDM:
* [!UICONTROL Select attributes]: utilizza questa opzione per mappare un campo specifico dallo schema XDM a un  [!DNL Braze] attributo.

![Attributo origine mappatura destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Utilizzare questa opzione per mappare uno spazio dei nomi  [!DNL Platform] di identità a uno  [!DNL Braze] spazio dei nomi.

![Spazio dei nomi dell&#39;origine della mappatura della destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Scegli il campo di origine, quindi fai clic su **[!UICONTROL Select]**.

Nella sezione [!UICONTROL Target Field] , fai clic sull’icona di mappatura a destra del campo .

![Mappatura del target di destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Nella finestra [!UICONTROL Select target field], puoi scegliere tra tre categorie di campi di destinazione:
* [!UICONTROL Select attributes]: Utilizza questa opzione per mappare gli attributi XDM su  [!DNL Braze] attributi standard.
* [!UICONTROL Select identity namespace]: Utilizzare questa opzione per mappare i namespace  [!DNL Platform] di identità agli spazi dei nomi  [!DNL Braze] di identità.
* [!UICONTROL Select custom attributes]: Utilizza questa opzione per mappare gli attributi XDM su  [!DNL Braze] attributi personalizzati definiti nel tuo  [!DNL Braze] account.
* Puoi inoltre utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Braze]. Ad esempio, se mappi un attributo `lastName` XDM su un attributo `Last_Name` personalizzato in [!DNL Braze], crea l&#39;attributo `Last_Name` in [!DNL Braze], se non esiste già, e mappalo sull&#39;attributo `lastName` XDM.

![Campi di mappatura destinazione di branding](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Scegli il campo di destinazione, quindi fai clic su **[!UICONTROL Select]**.

Ora dovresti vedere la mappatura dei campi nell’elenco.

![Mappatura destinazione del freno completata](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Per aggiungere altre mappature, ripeti i passaggi precedenti.

## Esempio di mappatura {#mapping-example}

Supponiamo che lo schema del profilo XDM e l’istanza [!DNL Braze] contengano i seguenti attributi ed identità:

|  | Schema del profilo XDM | [!DNL Braze] Istanza |
|---|---|---|
| Attributi | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identità | <ul><li>E-mail</code></li><li>Google Ad ID (GAID)</code></li><li>ID Apple per gli inserzionisti (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

La mappatura corretta sarà simile alla seguente:

![Esempio di mappatura della destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Braze], controlla il tuo account [!DNL Braze]. [!DNL Adobe Experience Platform] i segmenti vengono esportati in  [!DNL Braze] sotto l’ `AdobeExperiencePlatformSegments` attributo .

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta [Panoramica sulla governance dei dati](../../../data-governance/home.md).

