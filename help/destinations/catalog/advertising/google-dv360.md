---
keywords: Doppio clic su Gestione offerte;Doppio clic su Gestione offerte;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Destinazione Google Display e Video 360
seo-title: Destinazione Google Display e Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento che consente di eseguire campagne di retargeting e di targeting delle audience su diverse fonti di inventario di Display, Video e Mobile.
seo-description: 'Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento che consente di eseguire campagne di retargeting e di targeting delle audience su diverse fonti di inventario di Display, Video e Mobile. '
translation-type: tm+mt
source-git-commit: bb2fc2658d32c59b476dd9d526eb8bc2f055a1af
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destinazione

## Panoramica

[!DNL Display & Video 360], precedentemente noto come  [!DNL DoubleClick Bid Manager], è uno strumento utilizzato per eseguire il retargeting e le campagne digitali mirate per l&#39;audience tra le origini di inventario Display, Video e Mobile.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per le destinazioni [!DNL Google Display & Video 360]:

* È possibile inviare le seguenti [identità](../../../identity-service/namespaces.md) alle [!DNL Google Ads] destinazioni: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft e ID  Amazon Fire TV.
   * Google utilizzerà [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e il Google Cookie ID per tutti gli altri utenti.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* Al momento la piattaforma non include una metrica di misura per convalidare l&#39;attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Display &amp; Video 360 e non hai attivato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in  Experience Cloud ID Service in passato (con Adobe Audience Manager o altre applicazioni), contatta l&#39;Assistenza clienti o Adobe Consulenza   per abilitare le sincronizzazioni ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate configurato per il passaggio alla piattaforma.

### Tipo di esportazione {#export-type}

**Esportazione**  segmento: tutti i membri di un segmento (pubblico) vengono esportati nella destinazione Google.

## Prerequisiti

### elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di configurare la prima [!DNL Google Display & Video 360] destinazione in Platform. Prima di creare una destinazione, verificare che il processo di elenco consentiti  descritto di seguito sia stato completato da Google.

Prima di creare la destinazione [!DNL Google Display & Video 360] in Platform, è necessario contattare Google chiedendo che  Adobe sia inserito nell&#39;elenco dei provider di dati consentiti e che il tuo account sia aggiunto al elenco consentiti . Contattate Google e fornite le seguenti informazioni:

* **ID**  account: questo è  ID account  Adobe con Google. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **ID**  cliente: si tratta  ID account  cliente con Google. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **Tipo** account: utilizzate  **[!DNL Invite advertiser]** per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel vostro account Display &amp; Video 360 o  **[!DNL Invite partner]** per consentire ai tipi di pubblico di essere condivisi con tutti i marchi del vostro account Display &amp; Video 360.

## Configura destinazione

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Google Display & Video 360], quindi selezionare **[!UICONTROL Configure]**.

![Destinazione Google Display e Video 360 di Connect](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra [!UICONTROL Activate] e [!UICONTROL Configure], fare riferimento alla sezione [Catalog](../../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.

Nel passaggio **Setup** del flusso di lavoro di creazione della destinazione, compilare il [!UICONTROL Basic Information] per la destinazione, nonché i casi di utilizzo del marketing che devono essere applicati a tale destinazione.

![Informazioni di base Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: Selezionate un’opzione, a seconda dell’account con Google:
   * Utilizzate `Invite Advertiser` per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel vostro account Display &amp; Video 360.
   * Utilizzate `Invite Partner` per consentire la condivisione dei tipi di pubblico a tutti i marchi dell&#39;account Display &amp; Video 360.
* **[!UICONTROL Account ID]**: Compila il tuo  **[!DNL Invite partner]** o il tuo ID  **[!DNL Invite advertiser]** account con Google. In genere si tratta di un ID di sei o sette cifre.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, vedere la [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Quando si configura una destinazione [!DNL Google Display & Video 360], è necessario utilizzare il proprio [!DNL Google Account Manager] o  rappresentante del Adobe per capire quale tipo di account si dispone.

## Attivare i segmenti in [!DNL Google Display & Video 360]

Per istruzioni su come attivare i segmenti in [!DNL Google Display & Video 360], vedere [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Display & Video 360], controlla il tuo account [!DNL Google Display & Video 360]. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.