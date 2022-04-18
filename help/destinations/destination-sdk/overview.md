---
description: Adobe Experience Platform Destination SDK è un set di API di configurazione che ti consente di configurare pattern di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 7c6d0c8d4d1eea16f13359e9d7a895d767ad3c00
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

## Panoramica {#destinations-sdk}

Adobe Experience Platform Destination SDK è una suite di API di configurazione che ti consentono di configurare modelli di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.

La documentazione Destination SDK fornisce istruzioni per l’utilizzo di Adobe Experience Platform Destination SDK per configurare, testare e rilasciare un’integrazione di destinazione con Adobe Experience Platform e affinché la destinazione diventi parte del catalogo delle destinazioni in continua crescita.

![Panoramica del catalogo delle destinazioni](./assets/destinations-catalog-overview.png)

## Integrazioni personalizzate e prodotte {#productized-custom-integrations}

In qualità di partner di Destination SDK, puoi trarre vantaggio dall’aggiunta della destinazione per i prodotti al [catalogo Experience Platform](/help/destinations/catalog/overview.md):
1. Configurazioni di integrazione standardizzate tra i clienti con parametri preconfigurati e semplificate l’esperienza di configurazione per i clienti.
2. Presenta una scheda di destinazione con marchio nel catalogo delle destinazioni Experience Platform per semplificare la configurazione e la sensibilizzazione dei clienti.
3. È disponibile come integrazione di destinazione con Adobe Experience Platform e Real-time Customer Data Platform.

In qualità di cliente di Experience Platform, puoi creare una destinazione personalizzata personalizzata personalizzata specifica, in grado di soddisfare al meglio le tue esigenze di attivazione.

![Destination SDK diagramma visivo](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Tipi di integrazioni supportate {#supported-integration-types}

Tramite Destination SDK, Adobe Experience Platform supporta integrazioni in tempo reale con destinazioni con un endpoint API REST. L’integrazione in tempo reale con Experience Platform supporta funzionalità quali:
* Trasformazione e aggregazione dei messaggi
* Recupero profilo
* Integrazione dei metadati configurabile per inizializzare la configurazione del pubblico e il trasferimento dei dati
* Autenticazione configurabile
* Una suite di API di test e convalida per testare e iterare le configurazioni di destinazione

Leggi i requisiti tecnici sul lato destinazioni nel [prerequisiti per l’integrazione](./integration-prerequisites.md) articolo.


## Accesso alla Destination SDK {#get-access}

L’accesso alle Destination SDK varia in base al tuo stato di partner o cliente Experience Platform. Per ulteriori informazioni, consulta la tabella seguente.


| Tipo di partner o cliente | Come accedere alla Destination SDK |
---------|----------|
| Fornitore di software indipendente (ISV) | Partecipa a [Programma di scambio Adobe](https://partners.adobe.com/exchangeprogram/experiencecloud.html) e richiedere il provisioning di una sandbox Experience Platform per accedere a Destination SDK. |
| Integratore di sistema (SI) | Devi essere a livello Gold o Platinum nel [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html)e otterrai un Experience Platform di sandbox predisposto e l’accesso a Destination SDK. |
| Experience Platform del cliente sul [Pacchetto di attivazione](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | Per impostazione predefinita, puoi accedere alle sandbox e alle Destination SDK di Experience Platform. |
| Experience Platform del cliente sul [Pacchetto CDP in tempo reale](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Non disponi dell’accesso a Destination SDK, ma puoi accedere a tutte le destinazioni dei prodotti configurate da altre aziende che utilizzano Destination SDK e pubblicate tra le organizzazioni Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## Processo di alto livello {#process}

Il processo per configurare la destinazione nell’Experience Platform è descritto di seguito:

1. Se sei un ISV o un SI, consulta ottenere le informazioni di accesso nella sezione precedente. [Attivazione Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) I clienti possono saltare questo passaggio.
2. [Richiesta di provisioning di una sandbox di Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) e abilita l&#39;autorizzazione di authoring di destinazione.
3. [Creare l’integrazione](./configure-destination-instructions.md) seguendo la documentazione del prodotto.
4. [Verificare l’integrazione](./test-destination.md) seguendo la documentazione del prodotto.
5. [Invia l’integrazione](./submit-destination.md) ad Adobe, la revisione (il tempo di risposta standard è di cinque giorni lavorativi).
6. Se sei un ISV o un SI che crea un [integrazione di prodotti](./overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto sull’Experience League della destinazione.
7. Una volta approvata dall’Adobe, l’integrazione viene visualizzata nella [catalogo Experience Platform](/help/destinations/catalog/overview.md).
8. Per aggiornare l’integrazione, segui lo stesso processo.

## Riferimenti {#reference}

L’Adobe consiglia di leggere e comprendere i seguenti Experienci Platform di documentazione:

* [Panoramica sulle destinazioni Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base della composizione dello schema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Panoramica dello spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it)
