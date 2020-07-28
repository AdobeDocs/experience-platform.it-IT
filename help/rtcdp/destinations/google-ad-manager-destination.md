---
title: Destinazione Google Ad Manager
seo-title: Destinazione Google Ad Manager
description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
seo-description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Panoramica

[!DNL Google Ad Manager], precedentemente noto come [!DNL DoubleClick] per gli editori o [!DNL DoubleClick AdX], è una piattaforma di annunci da [!DNL Google] cui gli editori possono gestire la visualizzazione degli annunci sui propri siti Web, attraverso video e nelle app mobili.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per [!DNL Google Ad Manager] le destinazioni:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL Google Ad Manager] destinazioni: **ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella [!DNL Google] piattaforma.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ad Manager] e non hai attivato la funzionalità [di sincronizzazione](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  servizio ID Experience Cloud in passato (con  Audience Manager o altre applicazioni), contatta il servizio Consulenza Adobe o l&#39;Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevate impostato [!DNL Google] integrazioni in  Audience Manager, le sincronizzazioni ID configurate effettuavano il trasferimento ad Adobe Real-time CDP.

## Prerequisiti

### Elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di configurare la prima [!DNL Google Ad Manager] destinazione in Adobe Real-time CDP. Assicurarsi che il processo di elenco consentiti  descritto di seguito sia stato completato [!DNL Google] prima di creare una destinazione.

Prima di creare la [!DNL Google Ad Manager] destinazione in Adobe Real-time CDP, è necessario contattare Adobe [!DNL Google] per essere incluso nell&#39;elenco dei provider di dati consentiti e per aggiungere l&#39;account al elenco consentiti . Contattate [!DNL Google] e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** rete: questo è il tuo account con [!DNL Google Ad Manager]
* **ID** collegamento pubblico: questo è il tuo account con [!DNL Google Ad Manager]
* Il tipo di account. **DFP per Google** o **AdX buyer**.

## Crea destinazione

1. In **[!UICONTROL Connections > Destinations]**, selezionate [!DNL Google Ad Manager], quindi **[!UICONTROL Create destination]**.
   ![Connect, destinazione Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>

   ![Informazioni di base Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: Selezionate un’opzione, a seconda dell’account con Google:
   * Usa `DFP by Google` per [!DNL DoubleClick] editori
   * Usa `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Compila il tuo ID account con [!DNL Google]. Può trattarsi dell’ID di rete o dell’ID collegamento pubblico. In genere si tratta di un ID di otto cifre.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra i casi di utilizzo di marketing definiti da Adobe o creare un tuo caso di utilizzo di marketing. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti da Adobe, consulta la panoramica [dei criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

>[!NOTE]
>
> Per configurare una [!DNL Google Ad Manager] destinazione, contattate il vostro rappresentante [!DNL Google Account Manager] o Adobe per sapere quale tipo di account avete.

## Attiva i segmenti in [!DNL Google Ad Manager]

Per istruzioni su come attivare i segmenti in [!DNL Google Ad Manager], consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).