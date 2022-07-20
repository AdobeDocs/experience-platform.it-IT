---
keywords: Experience Platform;home;argomenti popolari;Adobe Experience Platform;guida API;guida API Platform;introduzione alla piattaforma;guida per gli sviluppatori
solution: Experience Platform
title: Postman in Adobe Experience Platform
topic-legacy: api guide
description: Questo documento contiene passaggi che descrivono come impostare un ambiente Postman, importare raccolte Postman e un elenco di raccolte disponibili per ogni servizio Platform.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: d06c3bc51909b464b9eed2a2f0df04ca531010b3
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman è una piattaforma di collaborazione per lo sviluppo API che consente di configurare ambienti con variabili preimpostate, condividere raccolte API, semplificare le richieste CRUD e altro ancora. La maggior parte dei servizi API di Platform dispone di raccolte Postman che possono essere utilizzate per facilitare l’esecuzione di chiamate API.

## Come impostare un ambiente Postman, ad Experience Platform

La seguente guida video illustra la creazione e la configurazione dell’ambiente Postman. Un ambiente Postman contiene tutte le intestazioni necessarie per effettuare chiamate API alle varie raccolte fornite di seguito. Una volta configurato, ogni volta che scade un valore (ad esempio `ACCESS_TOKEN`) è possibile aggiornare il valore corrente nell&#39;ambiente e questo nuovo valore viene utilizzato in tutte le raccolte.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Raccolte Postman {#collections}

Una cartella contenente tutte le raccolte Postman disponibili si trova da, visitando il [Experience Platform Postman: esempi dell’archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). In alternativa, un link di raccolta Postman può essere trovato in ogni singolo file swagger nel [Documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O.

Per scaricare una raccolta Postman, seleziona **[!DNL Raw]** dalla pagina GitHub per caricare il file JSON non elaborato in una nuova scheda. Quindi, fai clic con il pulsante destro del mouse e seleziona **[!DNL Save as]** per salvare il file in una destinazione locale di tua scelta.

![JSON raw](./images/api-guide/raw-collection.PNG)

## Importare una raccolta Postman {#import}

Per utilizzare un [Raccolta Postman](#collections), è necessario che sia configurato un ambiente. Una volta completata la configurazione dell’ambiente, seleziona la **[!DNL Manage Environments]** nell’angolo in alto a destra.

![gestione selettore ambiente](./images/api-guide/environment-selector.png)

Viene visualizzato un pover che visualizza tutti gli ambienti correnti. Per importare una raccolta, seleziona **[!DNL import]** .

![pulsante di importazione](./images/api-guide/import-collection.png)

Viene richiesto di scegliere un file da importare. Selezionare il file di raccolta Postman da importare. Una volta selezionata, la raccolta si popola nella barra a sinistra sotto la scheda Raccolte .

![raccolta popolata](./images/api-guide/imported-collection.png)

Ogni raccolta dispone di coppie chiave-valore diverse che possono essere necessarie per eseguire un&#39;operazione CRUD di successo. Controlla il servizio [Guida per gli sviluppatori API](api-guide.md#api-guides) per informazioni sui valori, suggerimenti e esempi richiesti.

Per ulteriori informazioni sull’interfaccia utente di Postman e sulle sue funzioni disponibili, visita il [Documentazione di Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Genera un token di accesso con Postman per uso non di produzione

>[!WARNING]
>
>Come indicato nella raccolta Postman di Identity Management Service (IMS), i metodi di generazione indicati sono adatti per **uso non di produzione**. La firma locale carica una libreria JavaScript da un host di terze parti e la firma remota invia la chiave privata a un servizio Web di proprietà e gestito da Adobe. Sebbene Adobe non memorizzi questa chiave privata, le chiavi di produzione non devono mai essere condivise con nessuno.

Il video seguente utilizza la [Raccolta Postman del servizio Identity Management (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) che può essere scaricato dall’archivio GitHub pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Passaggi successivi

In questo documento sono stati introdotti ambienti Postman, raccolte e modalità di importazione delle raccolte. Ora che Postman è pronto, visita il [Guida introduttiva a Platform](api-guide.md) per informazioni su intestazioni, esempi e un elenco obbligatori [Guide API](api-guide.md#api-guides) disponibile per ogni servizio Platform.
