---
title: Destinazione Google
seo-title: Destinazione Google
description: Adobe Real-time CDP si integra con Google per consentirvi di eseguire e attivare i dati attraverso DV360, Google Ad Manager, Google AdWords e Google AdX.
seo-description: Adobe Real-time CDP si integra con Google per consentirvi di eseguire e attivare i dati attraverso DV360, Google Ad Manager, Google AdWords e Google AdX.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Destinazione Google

## Panoramica

Adobe Real-time CDP si integra con Google per consentirvi di eseguire e attivare i dati attraverso DV360, Google Ad Manager, Google AdWords Display e Google AdX.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per le destinazioni Google:

* Potete inviare le seguenti [identità](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) alle destinazioni Google: ID cookie **Google, IDFA, GAID**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere il rilascio dei dati, fai riferimento ai conteggi delle audience in Google.

## Prerequisiti

### Whitelist

Prima di collegare la destinazione Google in Adobe Real-time CDP, è necessario contattare Google chiedendo che il vostro account sia inserito nella lista bianca. Contattate Google e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con Google. Per ottenere questo ID, contattate il supporto Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con Google. Per ottenere questo ID, contattate il supporto Adobe.
* **ID** partner: Questo è il tuo ID partner di tre cifre con Google;
* **ID** rete: questo è il tuo account con Google;
* **ID** collegamento pubblico: questo è il tuo account con Google;
* Il tipo di account. Questo potrebbe essere **Invita inserzionista**, **Invita partner**, **DFP**, **AdWords**, **AdX**.


## Destinazione Connect

1. In **[!UICONTROL Connessioni > Destinazioni]**, selezionate Google, quindi selezionate **[!UICONTROL Crea destinazione]**.
   ![Connect, destinazione Google](/help/rtcdp/destinations/assets/google-destination.png)

2. Nella procedura guidata di destinazione di Connect, compila le informazioni di base per la destinazione.
   ![Informazioni di base Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Nome**: Compila il nome preferito per questa destinazione.
* **Descrizione**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **Tipo** account: Selezionate un’opzione, a seconda dell’account con Google:
   * Utilizzate `Invite advertiser` per Google DV360
   * Utilizzate `Invite partner` per Google DV360
   * Usa `DFP by Google` per Google Ad Manager
   * Usa `AdWords` per Google AdWords Display
   * Usa `AdX buyer` per Google AdX
* **ID** account: Compila il tuo ID account con Google.

>[!NOTE]
>
>Per configurare una destinazione Google, contattate il vostro account manager Google o il rappresentante Adobe per capire quale tipo di prodotto rientra nel vostro account. Per Google DV360, chiedete al vostro account manager Google quale tipo di prodotto rientra nel campo di applicazione del vostro account. 

## Attivare i segmenti su Google

Per istruzioni su come attivare i segmenti in Google, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).