---
title: Destinazione Google Ad Manager
seo-title: Destinazione Google Ad Manager
description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
seo-description: 'Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili. '
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Destinazione Google Ad Manager

## Panoramica

Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di annunci pubblicitari di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti Web, attraverso video e nelle app mobili.

## Specifiche di destinazione

Tieni presente i seguenti dettagli specifici per le destinazioni Google Ad Manager:

* Puoi inviare le seguenti [identità](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) alle destinazioni Google Ad Manager: ID di cookie **Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Ad Manager e non hai attivato in passato la funzionalità [](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) di sincronizzazione ID nel servizio Experience Cloud ID (con Audience Manager o altre applicazioni), contatta Adobe Consulting o l’Assistenza clienti per abilitare la sincronizzazione ID. Se in precedenza avevate impostato le integrazioni Google in Audience Manager, le sincronizzazioni ID che avevate configurato riportano ad Adobe Real-time CDP.

## Prerequisiti

### Whitelist

>[!NOTE]
>
>La whitelist è obbligatoria prima di configurare la prima destinazione Google Ad Manager in Adobe Real-time CDP. Prima di creare una destinazione, verificare che il processo di whitelist descritto di seguito sia stato completato da Google.

Prima di creare la destinazione Google Ad Manager in Adobe Real-time CDP, è necessario contattare Google chiedendo che Adobe sia inserito nella lista bianca come provider di dati e che l&#39;account sia inserito nella lista bianca. Contattate Google e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** rete: questo è il tuo account con Google Ad Manager
* **ID** collegamento pubblico: questo è il tuo account con Google Ad Manager
* Il tipo di account. **DFP per Google** o **AdX buyer**.

## Crea destinazione

1. In **[!UICONTROL Connections > Destinations]**, seleziona Google Ad Manager e seleziona **[!UICONTROL Create destination]**.
   ![Connect, destinazione Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Nella procedura guidata Crea destinazione, compila le informazioni di base per la destinazione.
   ![Informazioni di base Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **Nome**: Compila il nome preferito per questa destinazione.
* **Descrizione**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **Tipo** account: Selezionate un’opzione, a seconda dell’account con Google:
   * Usa `DFP by Google` per doppio clic per gli editori
   * Usa `AdX buyer` per Google AdX
* **ID** account: Compila il tuo ID account con Google. Può trattarsi dell’ID di rete o dell’ID collegamento pubblico. In genere si tratta di un ID di otto cifre.

>[!NOTE]
>
>Quando configuri una destinazione Google Ad Manager, ti consigliamo di collaborare con il tuo account manager Google o con il rappresentante Adobe per capire quale tipo di account hai.

## Attivare i segmenti in Google Ad Manager

Per istruzioni su come attivare i segmenti in Google Ad Manager, consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).