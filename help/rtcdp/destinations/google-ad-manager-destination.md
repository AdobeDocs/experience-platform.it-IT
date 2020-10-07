---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager
title: Destinazione Google Ad Manager
seo-title: Destinazione Google Ad Manager
description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
seo-description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Panoramica

[!DNL Google Ad Manager], precedentemente noto come [!DNL DoubleClick] per gli editori o [!DNL DoubleClick AdX], è una piattaforma di annunci da [!DNL Google] cui gli editori possono gestire la visualizzazione degli annunci sui propri siti Web, attraverso video e nelle app mobili.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per [!DNL Google Ad Manager] le destinazioni:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL Google Ad Manager] destinazioni: **ID di cookie Google, IDFA, GAID, Roku ID, Microsoft ID,  Amazon Fire TV ID**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella [!DNL Google] piattaforma.
*  CDP in tempo reale del Adobe attualmente non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ad Manager] e non hai attivato la funzionalità [di sincronizzazione](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  Experience Cloud ID Service in passato (con  Audience Manager o altre applicazioni), contatta  Consulenza Adobe o l’Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevate impostato [!DNL Google] integrazioni in  Audience Manager, le sincronizzazioni ID che avevate impostato per il riporto  CDP in tempo reale del Adobe.

### Tipo esportazione {#export-type}

**Esportazione** segmento - vengono esportati tutti i membri di un segmento (pubblico) nella destinazione Google.

## Prerequisiti

### elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di impostare la prima [!DNL Google Ad Manager] destinazione  CDP in tempo reale Adobe. Assicurarsi che il processo di elenco consentiti  descritto di seguito sia stato completato [!DNL Google] prima di creare una destinazione.

Prima di creare la [!DNL Google Ad Manager] destinazione in CDP in tempo reale  Adobe, è necessario contattare [!DNL Google] affinché  Adobe venga inserito nell&#39;elenco dei provider di dati consentiti e che il vostro account venga aggiunto al elenco consentiti di . Contattate [!DNL Google] e fornite le seguenti informazioni:

* **ID** account:  ID account  Adobe con [!DNL Google]. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **ID** cliente: si tratta  ID account  cliente con [!DNL Google]. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **ID** rete: questo è il tuo account con [!DNL Google Ad Manager]
* **ID** collegamento pubblico: questo è il tuo account con [!DNL Google Ad Manager]
* Il tipo di account. DFP di Google o dell&#39;acquirente AdX.

## Configura destinazione

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare **[!DNL Google Ad Manager]**, quindi **[!UICONTROL Configure]**.
   ![Connect, destinazione Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>

   ![Informazioni di base Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: Selezionate un’opzione, a seconda dell’account con Google:
   * Usa `DFP by Google` per [!DNL DoubleClick] editori
   * Usa `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Compila il tuo ID account con [!DNL Google]. Può trattarsi dell’ID di rete o dell’ID collegamento pubblico. In genere si tratta di un ID di otto cifre.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

>[!NOTE]
>
> Per configurare una [!DNL Google Ad Manager] destinazione, rivolgetevi al rappresentante del Adobe [!DNL Google Account Manager] o  per capire quale tipo di account avete.

## Attiva i segmenti in [!DNL Google Ad Manager]

Per istruzioni su come attivare i segmenti in [!DNL Google Ad Manager], consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella [!DNL Google Ad Manager] destinazione, controlla il tuo [!DNL Google Ad Manager] account. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.