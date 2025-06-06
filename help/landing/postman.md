---
keywords: Experience Platform;home;argomenti popolari;Adobe Experience Platform;guida api;guida api piattaforma;introduzione alla piattaforma;guida per sviluppatori
solution: Experience Platform
title: Postman in Adobe Experience Platform
description: Questo documento contiene i passaggi che descrivono come impostare un ambiente Postman, importare raccolte Postman e un elenco delle raccolte disponibili per ciascun servizio Experience Platform.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman è una piattaforma di collaborazione per lo sviluppo di API che consente di configurare ambienti con variabili preimpostate, condividere raccolte API, semplificare le richieste CRUD e altro ancora. La maggior parte dei servizi API di Experience Platform dispone di raccolte Postman che possono essere utilizzate per facilitare l’esecuzione di chiamate API.

## Come impostare un ambiente Postman per Experience Platform

La seguente guida video illustra la creazione e la configurazione dell’ambiente Postman. Un ambiente Postman contiene tutte le intestazioni necessarie per effettuare chiamate API alle varie raccolte fornite di seguito. Dopo la configurazione, ogni volta che un valore scade (ad esempio `ACCESS_TOKEN`) puoi aggiornare il valore corrente nell&#39;ambiente e questo nuovo valore viene utilizzato in tutte le raccolte.

>[!VIDEO](https://video.tv.adobe.com/v/36258?captions=ita)

## Raccolte Postman {#collections}

È possibile trovare una cartella contenente tutte le raccolte Postman disponibili visitando l&#39;[archivio GitHub degli esempi di Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). In alternativa, è possibile trovare un collegamento alla raccolta Postman in ogni singolo file swagger nella [documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en) su Adobe I/O.

Per scaricare una raccolta Postman, seleziona **[!DNL Raw]** dalla pagina GitHub per caricare il file JSON non elaborato in una nuova scheda. Quindi, fare clic con il pulsante destro del mouse e selezionare **[!DNL Save as]** per salvare il file in una destinazione locale di propria scelta.

![JSON raw](./images/api-guide/raw-collection.PNG)

## Importare una raccolta Postman {#import}

Per utilizzare una [raccolta Postman](#collections), è necessario configurare un ambiente. Dopo aver completato la configurazione dell&#39;ambiente, seleziona il selettore **[!DNL Manage Environments]** nell&#39;angolo in alto a destra.

![gestisci selettore ambiente](./images/api-guide/environment-selector.png)

Viene visualizzato un popover che mostra tutti gli ambienti correnti. Per importare una raccolta, selezionare **[!DNL import]**.

![pulsante di importazione](./images/api-guide/import-collection.png)

Viene chiesto di scegliere un file da importare. Selezionare il file della raccolta Postman che si desidera importare. Una volta selezionata, la raccolta viene compilata nella barra a sinistra sotto la scheda Raccolte.

![raccolta popolata](./images/api-guide/imported-collection.png)

Ogni raccolta dispone di diverse coppie chiave-valore che potrebbero essere necessarie per eseguire un&#39;operazione CRUD riuscita. Per informazioni sui valori richiesti, suggerimenti e esempi, consulta la [guida per gli sviluppatori API](api-guide.md#api-guides) del servizio.

Per ulteriori informazioni sull&#39;interfaccia utente di Postman e sulle sue funzioni disponibili, consulta la [documentazione di Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generare un token di accesso con Postman per un utilizzo non di produzione

>[!WARNING]
>
>Come indicato nella raccolta Postman del servizio Identity Management (IMS), i metodi di generazione indicati sono adatti per **uso non di produzione**. La firma locale carica una libreria JavaScript da un host di terze parti e la firma remota invia la chiave privata a un servizio web di proprietà e gestito da Adobe. Anche se Adobe non memorizza questa chiave privata, le chiavi di produzione non devono mai essere condivise con nessuno.

Il video seguente utilizza la [raccolta Postman del servizio Identity Management (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) che può essere scaricata dall&#39;archivio GitHub pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/39133/?quality=12&learn=on&captions=ita)

## Passaggi successivi

Questo documento illustra ambienti, raccolte e come importare le raccolte di Postman. Ora che hai Postman pronto, visita la [guida introduttiva di Experience Platform](api-guide.md) per informazioni sulle intestazioni richieste, esempi e un elenco di [guide API](api-guide.md#api-guides) disponibili per ogni servizio Experience Platform.
