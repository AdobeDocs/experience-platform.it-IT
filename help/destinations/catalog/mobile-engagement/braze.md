---
keywords: mobile; brazo; messaggistica;
title: Destinazione del freno
seo-title: Destinazione del freno
description: Braze è una piattaforma completa di coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.
seo-description: Braze è una piattaforma completa di coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---


# (Beta) [!DNL Braze] destinazione

>[!IMPORTANT]
>
>La destinazione Braze in Adobe Experience Platform è attualmente in versione Beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

La destinazione [!DNL Braze] consente di inviare i dati del profilo a [!DNL Braze].

[!DNL Braze] è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.

Per inviare i dati del profilo a [!DNL Braze], è innanzitutto necessario connettersi alla destinazione.

## Specifiche di destinazione {#destination-specs}

Notate i seguenti dettagli specifici della destinazione [!DNL Braze]:

* È possibile inviare qualsiasi [identità](../../../identity-service/namespaces.md) alla destinazione [!DNL Braze], purché sia mappata sulla [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation).
* [!DNL Adobe Experience Platform] i segmenti vengono esportati in  [!DNL Braze] base all’ `AdobeExperiencePlatformSegments` attributo .

>[!NOTE]
>
>Tenere presente che l&#39;invio di attributi personalizzati aggiuntivi a [!DNL Braze] potrebbe causare aumenti nel consumo dei punti di dati [!DNL Braze]. Consultate il vostro account manager [!DNL Braze] prima di inviare attributi personalizzati aggiuntivi.

## Casi d’uso {#use-cases}

Come esperto di marketing, voglio indirizzare gli utenti verso una destinazione di coinvolgimento mobile, con i segmenti incorporati in [!DNL Adobe Experience Platform]. Inoltre, voglio fornire loro esperienze personalizzate, basate sugli attributi dai loro profili [!DNL Adobe Experience Platform], non appena segmenti e profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Tipo di esportazione {#export-type}

**[!DNL Profile-based]** - si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura del campo.
[!DNL Adobe Experience Platform] i segmenti vengono esportati in  [!DNL Braze] base all’ `AdobeExperiencePlatformSegments` attributo .


## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Braze], quindi selezionare **[!UICONTROL Configure]**.

![Configurare la destinazione del branco](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, fare riferimento alla sezione [Catalog](../../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.
>
>![Attiva destinazione di branding](../../assets/catalog/mobile-engagement/braze/activate.png)

Nel passaggio [!UICONTROL Account], è necessario fornire il token dell&#39;account [!DNL Braze]. Questo è il tasto [!DNL Braze] [!DNL API]. Per istruzioni dettagliate su come ottenere la chiave [!DNL API], consultate: [REST API Key Overview](https://www.braze.com/docs/api/api_key/). Immettete il token e fate clic su **[!UICONTROL Connect to destination]**.

![Passaggio dell&#39;account di destinazione del branding](../../assets/catalog/mobile-engagement/braze/account.png)

Fai clic su **[!UICONTROL Next]**. Nel passaggio [!UICONTROL Authentication], è necessario inserire i dettagli di connessione [!DNL Braze]:
* **[!UICONTROL Name]**: immettete un nome in base al quale riconoscerete questa destinazione in futuro.
* **[!UICONTROL Description]**: immettete una descrizione che vi aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Endpoint Instance]**: chiedete al vostro  [!DNL Braze] rappresentante quale istanza di endpoint utilizzare.
* **[!UICONTROL Marketing use case]**: i casi di utilizzo marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, vedere la pagina [Governance dei dati in Adobe Experience Platform](../../../data-governance/policies/overview.md). Per informazioni sui singoli casi d&#39;uso di marketing definiti dal Adobe , vedere la [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Passaggio di autenticazione del freno](../../assets/catalog/mobile-engagement/braze/authentication.png)

Fai clic su **[!UICONTROL Create destination]**. La destinazione è stata creata. È possibile fare clic su **[!UICONTROL Save & Exit]** se si desidera attivare i segmenti in un secondo momento, oppure è possibile selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, vedere la sezione successiva, [Attiva segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, vedere [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md#select-attributes).

## Mappatura dei campi {#field-mapping}

Per inviare correttamente i dati del pubblico da [!DNL Adobe Experience Platform] alla [!DNL Braze] destinazione, è necessario eseguire il passaggio di mappatura del campo.

Il mapping consiste nella creazione di un collegamento tra i campi dello schema [!DNL Experience Data Model] (XDM) nell&#39;account [!DNL Platform] e i corrispondenti equivalenti dalla destinazione.

Per mappare correttamente i campi XDM sui campi di destinazione [!DNL Braze], procedere come segue:

Nel passaggio [!UICONTROL Mapping], fare clic su **[!UICONTROL Add new mapping]**.

![Mappatura aggiunta destinazione di branding](../../assets/catalog/mobile-engagement/braze/mapping.png)

Nella sezione [!UICONTROL Source Field], fare clic sul pulsante freccia accanto al campo vuoto.

![Mappatura origine destinazione del branco](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Nella finestra [!UICONTROL Select source field], potete scegliere tra due categorie di campi XDM:
* [!UICONTROL Select attributes]: utilizzare questa opzione per mappare un campo specifico dallo schema XDM a un  [!DNL Braze] attributo.

![Attributo origine mappatura destinazione di branding](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Utilizzare questa opzione per mappare uno spazio nomi  [!DNL Platform] identità a uno  [!DNL Braze] spazio dei nomi.

![Spazio dei nomi di origine mappatura destinazione di branding](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Scegliete il campo di origine, quindi fate clic su **[!UICONTROL Select]**.

Nella sezione [!UICONTROL Target Field] fare clic sull&#39;icona di mappatura a destra del campo.

![Mappatura destinazione di destinazione del branco](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Nella finestra [!UICONTROL Select target field], potete scegliere tra tre categorie di campi di destinazione:
* [!UICONTROL Select attributes]: Utilizzate questa opzione per mappare gli attributi XDM su  [!DNL Braze] attributi standard.
* [!UICONTROL Select identity namespace]: Utilizzare questa opzione per mappare gli spazi dei nomi  [!DNL Platform] di identità agli spazi dei nomi  [!DNL Braze] di identità.
* [!UICONTROL Select custom attributes]: Utilizzate questa opzione per mappare gli attributi XDM su  [!DNL Braze] attributi personalizzati definiti nel vostro  [!DNL Braze] account.
* È inoltre possibile utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Braze]. Ad esempio, mappando un attributo `lastName` XDM su un attributo personalizzato `Last_Name` in [!DNL Braze], verrà creato l&#39;attributo `Last_Name` in [!DNL Braze], se non esiste già, e verrà mappato l&#39;attributo `lastName` XDM su di esso.

![Campi di mappatura destinazione di branding](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Scegliete il campo di destinazione, quindi fate clic su **[!UICONTROL Select]**.

È ora necessario visualizzare la mappatura dei campi nell&#39;elenco.

![Mappatura destinazione del freno completata](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Per aggiungere altre mappature, ripetere i passaggi precedenti.

### Esempio {#mapping-example}

Supponiamo che lo schema del profilo XDM e l&#39;istanza [!DNL Braze] contengano i seguenti attributi e identità:

|  | Schema profilo XDM | [!DNL Braze] Istanza |
|---|---|---|
| Attributi | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identità | <ul><li>E-mail</code></li><li>Google Ad ID (GAID)</code></li><li>ID Apple per inserzionisti (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

La mappatura corretta sarà simile alla seguente:

![Esempio di mappatura della destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Braze], controlla il tuo account [!DNL Braze]. [!DNL Adobe Experience Platform] i segmenti vengono esportati in  [!DNL Braze] base all’ `AdobeExperiencePlatformSegments` attributo .

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedere [Panoramica sulla governance dei dati](../../../data-governance/home.md).

