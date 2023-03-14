---
description: Adobe Experience Platform Destination SDK è un set di API di configurazione che ti consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire dati di pubblico e profilo all’endpoint o alla posizione di archiviazione, in base ai formati di dati e autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

## Panoramica {#destinations-sdk}

Adobe Experience Platform Destination SDK è una suite di API di configurazione che consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire dati di pubblico e profilo all’endpoint o alla posizione di archiviazione, in base ai formati di dati e autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.

La documentazione di Destination SDK fornisce istruzioni sull’utilizzo di Adobe Experience Platform Destination SDK per configurare, testare e rilasciare un’integrazione di destinazione prodotta con Adobe Experience Platform e per far sì che la destinazione diventi parte del catalogo delle destinazioni in continua crescita. Utilizzando Destination SDK, puoi anche creare una destinazione privata personalizzata per esportare dati personalizzati in base alle tue esigenze.

![Schermata dall’interfaccia utente di Experience Platform che mostra il catalogo delle destinazioni](./assets/destinations-catalog-overview.png)

## Integrazioni prodotte e personalizzate {#productized-custom-integrations}

>[!IMPORTANT]
>
> Questa funzionalità per creare destinazioni personalizzate private è disponibile solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

In qualità di partner di Destination SDK, puoi trarre vantaggio dall’aggiunta della destinazione prodotta al [catalogo Experienci Platform](/help/destinations/catalog/overview.md):
1. Standardizzare le configurazioni di integrazione tra i clienti con parametri preconfigurati e semplificare l’esperienza di configurazione per i clienti.
2. Per semplificare la configurazione e la conoscenza dei clienti, introduce una scheda di destinazione con marchio nel catalogo delle destinazioni di Experience Platform.
3. Essere presentata come integrazione di destinazione prodotta con Adobe Experience Platform e Adobe Real-time Customer Data Platform.

In qualità di cliente Experience Platform, puoi anche creare una destinazione personalizzata privata, che può soddisfare al meglio le tue esigenze di attivazione.

![Un diagramma di panoramica che mostra come gli sviluppatori di destinazione interagiscono con Destination SDK e come i clienti Real-Time CDP traggono vantaggio dalle destinazioni prodotte e private.](./assets/destination-sdk-visual.png)

## Tipi di integrazioni supportate {#supported-integration-types}

Tramite Destination SDK, Adobe Experience Platform supporta integrazioni in tempo reale con destinazioni che hanno un endpoint REST API. L’integrazione in tempo reale con Experience Platform supporta funzionalità quali:
* Trasformazione e aggregazione dei messaggi
* Recupero profilo
* Integrazione dei metadati configurabile per inizializzare la configurazione del pubblico e il trasferimento dei dati
* Autenticazione configurabile
* Una suite di API di test e convalida per testare e ripetere le configurazioni di destinazione

Tramite Destination SDK è inoltre possibile configurare integrazioni per esportare periodicamente i file nel percorso di archiviazione desiderato. L’integrazione in tempo reale con Experience Platform supporta funzionalità quali:
* Esportazione di file in diversi formati supportati (CSV, Parquet, JSON)
* Opzioni di formattazione del file configurabili, che consentono di strutturare il formato dei file esportati in base ai requisiti downstream.

Scopri i requisiti tecnici per le destinazioni nella sezione [prerequisiti per l’integrazione](./integration-prerequisites.md) articolo.

## Accedere a Destination SDK {#get-access}

L’accesso Destination SDK varia in base al tuo stato di partner o Experience Platform, cliente Real-Time CDP. Per ulteriori informazioni, consulta la tabella seguente.


| Tipo di partner o cliente | Come accedere a Destination SDK |
---------|----------|
| Fornitore indipendente di software (ISV) | Partecipa a [Programma Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud.html) e per ottenere un Experience Platform di sandbox per l’accesso a Destination SDK. |
| Integratore di sistemi (SI) | È necessario essere a livello Gold o Platinum nel [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html), e otterrai una sandbox di Experience Platform con provisioning e accesso a Destination SDK. |
| Experience Platform del cliente su [Pacchetto Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Per impostazione predefinita, hai accesso ad Experience Platform sandbox e Destination SDK, che ti consentono di creare destinazioni private per la tua organizzazione. |

{style="table-layout:auto"}

## Processo di alto livello {#process}

Di seguito è descritta la procedura per configurare la destinazione in Experience Platform:

1. Se sei un ISV o un SI, consulta la sezione precedente per informazioni sull’accesso. [Attivazione Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) I clienti possono saltare questo passaggio.
2. [Richiesta di provisioning di una sandbox di Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) e abilita l’autorizzazione di authoring della destinazione.
3. Crea la tua integrazione. Segui le istruzioni riportate nella documentazione del prodotto per configurare [destinazioni di streaming](./configure-destination-instructions.md) o [destinazioni basate su file](./configure-file-based-destination-instructions.md).
4. Verifica l’integrazione. Segui le istruzioni riportate nella documentazione del prodotto per eseguire il test [destinazioni di streaming](./test-destination.md) o [destinazioni basate su file](./file-based-destination-testing-overview.md).
5. Se sei un ISV o un SI che crea un [integrazione di produzione](./overview.md#productized-custom-integrations), [invia la tua integrazione](./submit-destination.md) ad Adobe, la revisione (il tempo di risposta standard è di cinque giorni lavorativi).
6. Se sei un ISV o un SI che crea un’integrazione prodotta, utilizza [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto su Experience League per la tua destinazione.
7. Per le integrazioni prodotte, una volta approvate da Adobe, l’integrazione verrà visualizzata in [catalogo Experienci Platform](/help/destinations/catalog/overview.md).
8. Se desideri aggiornare l’integrazione, segui la stessa procedura.

## Riferimenti {#reference}

L’Adobe consiglia di leggere e comprendere la seguente documentazione di Experience Platform:

* [Panoramica sulle destinazioni di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base della composizione dello schema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it)
* [Panoramica sullo spazio dei nomi delle identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it)
