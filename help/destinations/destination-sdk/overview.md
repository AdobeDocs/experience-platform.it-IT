---
description: Adobe Experience Platform Destination SDK è un set di API di configurazione che ti consentono di configurare pattern di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione desiderati. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.
title: SDK per destinazione Adobe Experience Platform
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 2%

---

# SDK per destinazione Adobe Experience Platform

## Panoramica {#destinations-sdk}

Adobe Experience Platform Destination SDK è una suite di API di configurazione che ti consentono di configurare pattern di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione desiderati. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.

La documentazione dell’SDK di destinazione fornisce istruzioni per l’utilizzo dell’SDK di destinazione Adobe Experience Platform per configurare, testare e rilasciare un’integrazione di destinazione di prodotto con Adobe Experience Platform e affinché la destinazione diventi parte del catalogo delle destinazioni in continua crescita.

![Panoramica del catalogo delle destinazioni](./assets/destinations-catalog-overview.png)

## Integrazioni personalizzate e prodotte {#productized-custom-integrations}

In qualità di partner SDK di destinazione, puoi sfruttare l&#39;aggiunta della destinazione di prodotto al [catalogo di Experience Platform](/help/destinations/catalog/overview.md):
1. Configurazioni di integrazione standardizzate tra i clienti con parametri preconfigurati e semplificate l’esperienza di configurazione per i clienti.
2. Presenta una scheda di destinazione con marchio nel catalogo delle destinazioni Experience Platform per semplificare la configurazione e la sensibilizzazione dei clienti.
3. È disponibile come integrazione di destinazione per i prodotti con Adobe Experience Platform e Real-time Customer Data Platform.

In qualità di cliente di Experience Platform, puoi creare una destinazione personalizzata personalizzata personalizzata specifica, in grado di soddisfare al meglio le tue esigenze di attivazione.

![Diagramma visivo dell’SDK di destinazione](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Tipi di integrazioni supportate {#supported-integration-types}

Attraverso l’SDK di destinazione, Adobe Experience Platform supporta integrazioni in tempo reale con destinazioni con un endpoint API REST. L’integrazione in tempo reale con Experience Platform supporta funzionalità quali:
* Trasformazione e aggregazione dei messaggi
* Recupero profilo
* Integrazione dei metadati configurabile per inizializzare la configurazione del pubblico e il trasferimento dei dati
* Autenticazione configurabile
* Una suite di API di test e convalida per testare e iterare le configurazioni di destinazione

Leggi i requisiti tecnici sul lato destinazioni nell&#39;articolo [prerequisiti per l&#39;integrazione](./integration-prerequisites.md) .


## Accedere all’SDK di destinazione {#get-access}

L&#39;accesso all&#39;SDK di destinazione varia a seconda dello stato come cliente di un partner o di un Experience Platform. Per ulteriori informazioni, consulta la tabella seguente.


| Tipo di partner o cliente | Come accedere all’SDK di destinazione |
---------|----------|
| Fornitore di software indipendente (ISV) | Partecipa al [programma Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud.html) e richiedi il provisioning di una sandbox di Experience Platform per accedere all&#39;SDK di destinazione. |
| Integratore di sistema (SI) | È necessario essere a livello Gold o Platinum nel [programma Adobe Solution Partner](https://solutionpartners.adobe.com/home.html) e otterrai un Experience Platform di provisioning sandbox e l&#39;accesso all&#39;SDK di destinazione. |
| Experience Platform del cliente sul pacchetto Activation | Per impostazione predefinita, puoi accedere alle sandbox di Experience Platform e all’SDK di destinazione. |
| Experience Platform di clienti sul pacchetto Real-time CDP | Non hai accesso all’SDK di destinazione, ma hai accesso a tutte le destinazioni prodotti configurate da altre aziende che utilizzano l’SDK di destinazione e pubblicate tra le organizzazioni Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## Processo di alto livello {#process}

Il processo per configurare la destinazione nell’Experience Platform è descritto di seguito:

1. Se sei un ISV o un SI, consulta ottenere le informazioni di accesso nella sezione precedente. [I clienti di Adobe Experience Platform ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Activationpossono saltare questo passaggio.
2. [Richiesta di provisioning di una ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) sandbox di Experience Platform e abilitazione dell’autorizzazione di authoring di destinazione.
3. [Crea la tua ](./configure-destination-instructions.md) integrazione seguendo la documentazione del prodotto.
4. [Verifica l’](./test-destination.md) integrazione seguendo la documentazione del prodotto.
5. [Invia l’](./destination-publish-api.md) integrazione per la revisione di Adobe (il tempo di risposta standard è di 5 giorni lavorativi).
6. Se sei un ISV o un SI che crea un [integrazione prodotta](./overview.md#productized-custom-integrations), utilizza il [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto sull&#39;Experience League della tua destinazione.
7. Una volta approvata dall&#39;Adobe, l&#39;integrazione verrà visualizzata nel [catalogo di Experience Platform](/help/destinations/catalog/overview.md).
8. Per aggiornare l’integrazione, segui lo stesso processo.

## Riferimenti {#reference}

L’Adobe consiglia di leggere e comprendere i seguenti Experienci Platform di documentazione:

* [Panoramica sulle destinazioni Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base della composizione dello schema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Panoramica dello spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
