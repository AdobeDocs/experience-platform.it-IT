---
title: Destinazione Google Ad Manager
seo-title: Destinazione Google Ad Manager
description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
seo-description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---


# Destinazione Google Ad Manager

## Panoramica

Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili.

## Specifiche di destinazione

Tieni presente i seguenti dettagli specifici per le destinazioni Google Ad Manager:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle destinazioni Google Ad Manager: **ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Ad Manager e non hai attivato la funzionalità [di sincronizzazione degli](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  Experience Cloud ID Service in passato (con  Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate configurato riportano ad Adobe Real-time CDP.

## Prerequisiti

### Consenti elenco

>[!NOTE]
>
>L&#39;elenco di autorizzazioni è obbligatorio prima di configurare la prima destinazione Google Ad Manager in Adobe Real-time CDP. Prima di creare una destinazione, verificare che la procedura di autorizzazione elenco descritta di seguito sia stata completata da Google.

Prima di creare la destinazione Google Ad Manager in Adobe Real-time CDP, è necessario contattare Google per inserire Adobe nell&#39;elenco dei provider di dati consentiti e per aggiungere l&#39;account all&#39;elenco dei provider consentiti. Contattate Google e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** rete: questo è il tuo account con Google Ad Manager
* **ID** collegamento pubblico: questo è il tuo account con Google Ad Manager
* Il tipo di account. **DFP per Google** o **AdX buyer**.

## Crea destinazione

1. In **[!UICONTROL Connections > Destinations]**, seleziona Google Ad Manager e seleziona **[!UICONTROL Create destination]**.
   ![Connect, destinazione Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>
   ![Informazioni di base Google Ad Manager](/help/rtcdp/destinations/assets/ad-manager-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: Selezionate un’opzione, a seconda dell’account con Google:
   * Usa `DFP by Google` per doppio clic per gli editori
   * Usa `AdX buyer` per Google AdX
* **[!UICONTROL Account ID]**: Compila il tuo ID account con Google. Può trattarsi dell’ID di rete o dell’ID collegamento pubblico. In genere si tratta di un ID di otto cifre.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra i casi di utilizzo di marketing definiti da Adobe oppure creare un tuo caso di utilizzo di marketing. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti da Adobe, consulta la panoramica [dei criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

> [!NOTE]
>
> Quando configuri una destinazione Google Ad Manager, ti consigliamo di collaborare con il tuo account manager Google o con il rappresentante Adobe per capire quale tipo di account hai.

## Attivare i segmenti in Google Ad Manager

Per istruzioni su come attivare i segmenti in Google Ad Manager, consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).