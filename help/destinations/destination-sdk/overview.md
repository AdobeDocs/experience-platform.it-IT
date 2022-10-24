---
description: Adobe Experience Platform Destination SDK è un set di API di configurazione che ti consente di configurare pattern di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint o alla posizione di archiviazione, in base ai dati e ai formati di autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

## Panoramica {#destinations-sdk}

Adobe Experience Platform Destination SDK è una suite di API di configurazione che ti consente di configurare i pattern di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint o alla posizione di archiviazione, in base ai dati e ai formati di autenticazione scelti. Le configurazioni sono memorizzate in Experience Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.

La documentazione Destination SDK fornisce istruzioni per l’utilizzo di Adobe Experience Platform Destination SDK per configurare, testare e rilasciare un’integrazione di destinazione con Adobe Experience Platform e affinché la destinazione diventi parte del catalogo delle destinazioni in continua crescita. Utilizzando Destination SDK, puoi anche creare una destinazione privata personalizzata per esportare dati personalizzati in base alle tue esigenze.

![Schermata dall’interfaccia utente Experience Platform, che mostra il catalogo delle destinazioni](./assets/destinations-catalog-overview.png)

## Integrazioni personalizzate e prodotte {#productized-custom-integrations}

>[!IMPORTANT]
>
> Questa funzionalità per creare destinazioni personalizzate private è disponibile solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

In qualità di partner di Destination SDK, puoi trarre vantaggio dall’aggiunta della destinazione per i prodotti al [catalogo Experience Platform](/help/destinations/catalog/overview.md):
1. Configurazioni di integrazione standardizzate tra i clienti con parametri preconfigurati e semplificate l’esperienza di configurazione per i clienti.
2. Presenta una scheda di destinazione con marchio nel catalogo delle destinazioni Experience Platform per semplificare la configurazione e la sensibilizzazione dei clienti.
3. È disponibile come integrazione di destinazione per i prodotti con Adobe Experience Platform e Adobe Real-time Customer Data Platform.

In qualità di cliente di Experience Platform, puoi anche creare una destinazione personalizzata privata, che può soddisfare al meglio le tue esigenze di attivazione.

![Un diagramma di panoramica che mostra come gli sviluppatori di destinazioni interagiscono con Destination SDK e come i clienti Real-Time CDP traggono vantaggio dalle destinazioni produttive e private.](./assets/destination-sdk-visual.png)

## Tipi di integrazioni supportate {#supported-integration-types}

Tramite Destination SDK, Adobe Experience Platform supporta integrazioni in tempo reale con destinazioni con un endpoint API REST. L’integrazione in tempo reale con Experience Platform supporta funzionalità quali:
* Trasformazione e aggregazione dei messaggi
* Recupero profilo
* Integrazione dei metadati configurabile per inizializzare la configurazione del pubblico e il trasferimento dei dati
* Autenticazione configurabile
* Una suite di API di test e convalida per testare e iterare le configurazioni di destinazione

Tramite Destination SDK è inoltre possibile impostare integrazioni per esportare periodicamente i file nel percorso di archiviazione desiderato. L’integrazione in tempo reale con Experience Platform supporta funzionalità quali:
* Esportazione di file in diversi formati supportati (CSV, Parquet, JSON)
* Opzioni di formattazione dei file configurabili, che consentono di strutturare il formato dei file esportati in modo da soddisfare i requisiti downstream.

Leggi i requisiti tecnici sul lato destinazioni nel [prerequisiti per l’integrazione](./integration-prerequisites.md) articolo.

## Accesso alla Destination SDK {#get-access}

L’accesso alle Destination SDK varia a seconda dello stato in cui si è partner o, ad Experience Platform, cliente Real-Time CDP. Per ulteriori informazioni, consulta la tabella seguente.


| Tipo di partner o cliente | Come accedere alla Destination SDK |
---------|----------|
| Fornitore di software indipendente (ISV) | Partecipa a [Programma di scambio Adobe](https://partners.adobe.com/exchangeprogram/experiencecloud.html) e richiedere il provisioning di una sandbox Experience Platform per accedere a Destination SDK. |
| Integratore di sistema (SI) | Devi essere a livello Gold o Platinum nel [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html)e otterrai un Experience Platform di sandbox predisposto e l’accesso a Destination SDK. |
| Experience Platform del cliente sul [Pacchetto Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Per impostazione predefinita, puoi accedere alle sandbox e alla Destination SDK di Experience Platform, per creare destinazioni private per la tua organizzazione. |

{style=&quot;table-layout:auto&quot;}

## Processo di alto livello {#process}

Il processo per configurare la destinazione nell’Experience Platform è descritto di seguito:

1. Se sei un ISV o un SI, consulta ottenere le informazioni di accesso nella sezione precedente. [Attivazione Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) I clienti possono saltare questo passaggio.
2. [Richiesta di provisioning di una sandbox di Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) e abilita l&#39;autorizzazione di authoring di destinazione.
3. Genera la tua integrazione. Segui le istruzioni contenute nella documentazione del prodotto per configurare [destinazioni di streaming](./configure-destination-instructions.md) o [destinazioni basate su file](./configure-file-based-destination-instructions.md).
4. Verifica l’integrazione. Segui le istruzioni riportate nella documentazione del prodotto per eseguire il test [destinazioni di streaming](./test-destination.md) o [destinazioni basate su file](./file-based-destination-testing-overview.md).
5. Se sei un ISV o un SI che crea un [integrazione di prodotti](./overview.md#productized-custom-integrations), [invia integrazione](./submit-destination.md) per la revisione di Adobe (il tempo di risposta standard è di cinque giorni lavorativi).
6. Se sei un ISV o un SI che crea un’integrazione di prodotto, utilizza il [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto sull’Experience League della destinazione.
7. Per le integrazioni prodotte, una volta approvata da Adobe, l’integrazione verrà visualizzata nella [catalogo Experience Platform](/help/destinations/catalog/overview.md).
8. Se desideri aggiornare l’integrazione, segui lo stesso processo.

## Riferimenti {#reference}

L’Adobe consiglia di leggere e comprendere i seguenti Experienci Platform di documentazione:

* [Panoramica sulle destinazioni Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base della composizione dello schema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it)
* [Panoramica dello spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it)
