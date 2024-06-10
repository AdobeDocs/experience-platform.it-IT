---
description: Adobe Experience Platform Destination SDK è un set di API di configurazione che ti consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire dati di pubblico e profilo all’endpoint o alla posizione di archiviazione, in base ai formati di dati e autenticazione scelti. Le configurazioni sono memorizzate in Experienci Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 9c59f6edd51c61c1fe2ff69e0adea49e6efb8745
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK è una suite di API di configurazione che consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire dati di pubblico e profilo all’endpoint o alla posizione di archiviazione, in base ai formati di dati e autenticazione scelti. Le configurazioni sono memorizzate in Experienci Platform e possono essere recuperate tramite API per ulteriori aggiornamenti.

La documentazione di Destination SDK fornisce istruzioni sull’utilizzo del Adobe Experience Platform Destination SDK per configurare, testare e rilasciare un’integrazione di destinazione prodotta con Adobe Experience Platform e per far sì che la destinazione diventi parte del catalogo delle destinazioni in continua crescita. Utilizzando Destination SDK, puoi anche creare una destinazione privata personalizzata per esportare dati personalizzati in base alle tue esigenze.

![Schermata dall’interfaccia utente di Experienci Platform che mostra il catalogo delle destinazioni.](assets/destinations-catalog-overview.png)

## Guida rapida: esplorare le informazioni essenziali {#quick-start}

Consulta la documentazione nei collegamenti riportati di seguito per iniziare rapidamente a configurare e inviare la destinazione tramite Destination SDK.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Pagine di configurazione</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Spiegazione di tutte le opzioni di configurazione</a></li>
                <li> Configurazione del server di destinazione - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">specifiche del server</a> e <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">specifiche modelli</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Campi dati del cliente e altri componenti di configurazione della destinazione</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Modellazione e macro</a></li>
            </ul>
        </td>
        <td>
            <p><b>Guide</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Processo di integrazione di alto livello</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Configurare una destinazione di streaming</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Configurare una destinazione basata su file</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Configurare una destinazione per esportare i profili di prospect</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Invia destinazione per la pubblicazione</a></li>
            </ul>
        </td>
                <td>
            <p><b>Riferimenti API</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">Riferimento API per endpoint server di destinazione</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">Riferimento API per l’endpoint di destinazione</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">Riferimento API per i metadati del pubblico</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">Riferimento API del test</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">Riferimento API per la pubblicazione della destinazione</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Configurare una destinazione di streaming - Scheda di riferimento rapido</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Configurare una guida end-to-end per la destinazione di streaming</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">Comprendere la trasformazione dei dati tramite i modelli di Pebble</a> e <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">visualizzare le funzioni di modello supportate</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Comprendere i criteri di aggregazione dei dati</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Esempio di configurazione live</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Verifica la destinazione di streaming</a></li>
            </ul>
        </td>
        <td>
            <p><b>Configurare una destinazione basata su file - Scheda di riferimento rapido</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Configurare una guida end-to-end per una destinazione basata su file</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Configurare i formati di file per i file esportati</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Esempio di configurazione live per una destinazione Amazon S3</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">Configurazione batch</a> per la pianificazione dell'esportazione e la denominazione dei file</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Test della destinazione basata su file</a></li>
            </ul>
        </td>
        <td>
            <p><b>Altre informazioni essenziali</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Ottenere le credenziali di autenticazione richieste per utilizzare l’API</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Prerequisiti per l’integrazione</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Glossario dei termini di Destination SDK</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Limiti di frequenza e criteri per nuovi tentativi</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Modello self-service per documentare la destinazione</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## Integrazioni prodotte e personalizzate {#productized-custom-integrations}

>[!IMPORTANT]
>
> Questa funzionalità per creare destinazioni personalizzate private è disponibile solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

In qualità di partner di Destination SDK, puoi trarre vantaggio dall’aggiunta della destinazione prodotta al [catalogo Experienci Platform](../catalog/overview.md):

1. Standardizzare le configurazioni di integrazione tra i clienti con parametri preconfigurati e semplificare l’esperienza di configurazione per i clienti.
2. Per semplificare la configurazione e la conoscenza dei clienti, introduce una scheda di destinazione con marchio nel catalogo delle destinazioni di Experience Platform.
3. Essere presentata come integrazione di destinazione prodotta con Adobe Experience Platform e Adobe Real-time Customer Data Platform.

In qualità di cliente Experience Platform, puoi anche creare una tua destinazione personalizzata privata, che può soddisfare al meglio le tue esigenze di attivazione.

![Diagramma di panoramica che mostra come gli sviluppatori di destinazione interagiscono con Destination SDK e come i clienti Real-Time CDP traggono vantaggio dalle destinazioni prodotte e private.](assets/destination-sdk-visual.png)

## Tipi di integrazione supportati {#supported-integration-types}

### Integrazioni in tempo reale (streaming) {#real-time-integrations}

Tramite Destination SDK, Adobe Experience Platform supporta integrazioni in tempo reale (o streaming) con destinazioni che hanno un endpoint REST API. L’integrazione in tempo reale con Experienci Platform supporta funzionalità quali:

* Trasformazione e aggregazione dei messaggi
* Recupero profilo
* Integrazione dei metadati configurabile per inizializzare la configurazione del pubblico e il trasferimento dei dati
* Autenticazione configurabile
* Una suite di API di test e convalida per testare e ripetere le configurazioni di destinazione

### Integrazioni basate su file {#file-based-integrations}

Tramite Destination SDK è inoltre possibile configurare integrazioni per esportare periodicamente i file nel percorso di archiviazione desiderato. L’integrazione basata su file con Experienci Platform supporta funzionalità quali:

* Esportazione di file in diversi formati supportati (CSV, Parquet, JSON)
* Opzioni di formattazione del file configurabili, che consentono di strutturare il formato dei file esportati in base ai requisiti downstream.

Scopri i requisiti tecnici per le destinazioni nella sezione [prerequisiti per l’integrazione](integration-prerequisites.md) e leggi tutte le configurazioni supportate in [opzioni di configurazione](functionality/configuration-options.md) articolo

## Accedere a Destination SDK {#get-access}

L’accesso Destination SDK varia in base al tuo stato di partner o Experience Platform, cliente Real-Time CDP. Per ulteriori informazioni, consulta la tabella seguente.

| Tipo di partner o cliente | Come accedere a Destination SDK |
---------|----------|
| Fornitore indipendente di software (ISV) | Partecipa a [Programma Adobe Technology Partner](https://partners.adobe.com/technologyprogram/experiencecloud.html) e per ottenere un Experience Platform di sandbox per l’accesso a Destination SDK. |
| Integratore di sistemi (SI) | È necessario essere a livello Gold o Platinum nel [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html) per ottenere il provisioning di una sandbox di Experience Platform e l’accesso a Destination SDK. |
| Experience Platform del cliente su [Pacchetto Real-Time CDP Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) | Per impostazione predefinita, hai accesso ad Experienci Platform sandbox e Destination SDK, che ti consentono di creare destinazioni private per la tua organizzazione. |

{style="table-layout:auto"}

## Processo di alto livello {#process}

Di seguito è descritta la procedura per configurare la destinazione in Experienci Platform:

1. Se si è un ISV o un SI, vedere [accesso in corso](#get-access) informazioni nella sezione precedente. [Pacchetto Real-Time CDP Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) I clienti possono saltare questo passaggio.
2. [Richiesta di provisioning di una sandbox di Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) e abilita l’autorizzazione di authoring della destinazione.
3. Crea la tua integrazione. Segui le istruzioni riportate nella documentazione del prodotto per configurare [destinazioni di streaming](guides/configure-destination-instructions.md) o [destinazioni basate su file](guides/configure-file-based-destination-instructions.md).
4. Verifica l’integrazione. Segui le istruzioni riportate nella documentazione del prodotto per eseguire il test [destinazioni di streaming](testing-api/streaming-destinations/streaming-destination-testing-overview.md) o [destinazioni basate su file](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Se sei un ISV o un SI che crea un [integrazione di produzione](./overview.md#productized-custom-integrations), [invia la tua integrazione](guides/submit-destination.md) ad Adobe, la revisione (il tempo di risposta standard è di cinque giorni lavorativi).
6. Se sei un ISV o un SI che crea un’integrazione prodotta, utilizza [processo di documentazione self-service](docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto su Experience League per la tua destinazione.
7. Per le integrazioni prodotte, una volta approvate da Adobe, l’integrazione verrà visualizzata in [catalogo Experienci Platform](../catalog/overview.md).
8. Se desideri aggiornare l’integrazione, segui la stessa procedura.

## Riferimenti {#reference}

L’Adobe consiglia di leggere e comprendere la seguente documentazione di Experience Platform:

* [Panoramica sulle destinazioni di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=it)
* [Base della composizione dello schema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it)
* [Panoramica sullo spazio dei nomi delle identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it)
