---
title: Esempio Di Scenari Cliente Risolti Dalle Regole Di Collegamento Del Grafico Delle Identità
description: Scopri scenari di clienti di esempio risolti dalle regole di collegamento del grafico delle identità.
badge: Beta
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: be6fdb7e23ed4769ab4ee7ef72532296f020f4a4
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# Esempi di scenari cliente risolti dalle regole di collegamento del grafico delle identità

>[!AVAILABILITY]
>
>Questa funzione non è ancora disponibile; il programma beta per le regole di collegamento del grafo delle identità dovrebbe iniziare a luglio per le sandbox di sviluppo. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione.

Questo documento illustra alcuni scenari di esempio da considerare durante la configurazione delle regole di collegamento del grafico delle identità.

## Dispositivo condiviso

Esistono casi in cui si possono verificare più accessi su un singolo dispositivo:

| Dispositivo condiviso | Descrizione |
| --- | --- |
| Family computer e tablet | Marito e moglie accedono entrambi ai rispettivi conti bancari. |
| Chiosco pubblico | I viaggiatori che si registrano in aeroporto utilizzando il proprio ID fedeltà per effettuare il check-in delle borse e stampare le carte d’imbarco. |
| Call center | Il personale del call center accede a un singolo dispositivo per conto dei clienti che chiamano l’assistenza clienti per risolvere i problemi. |

![dispositivi condivisi](../images/identity-settings/shared-devices.png)

In questi casi, dal punto di vista del grafico, senza limiti abilitati, un singolo ECID sarà collegato a più CRMID.

Con le regole di collegamento del grafico delle identità, puoi:

* Configura l’ID utilizzato per l’accesso come identificatore univoco. Ad esempio, puoi limitare un grafico per memorizzare una sola identità con uno spazio dei nomi CRMID e quindi definire tale CRMID come identificatore univoco di un dispositivo condiviso.
   * In questo modo, puoi evitare che i CRMID vengano uniti dall’ECID.

## Scenari e-mail/telefono non validi

Ci sono anche esempi di utenti che forniscono valori falsi come numeri di telefono e/o indirizzi e-mail al momento della registrazione. In questi casi, se i limiti non sono abilitati, le identità relative a telefono/e-mail finiranno per essere collegate a più CRMID diversi.

![email-phone non valido](../images/identity-settings/invalid-email-phone.png)

Con le regole di collegamento del grafico delle identità, puoi:

* Configura il CRMID, il numero di telefono o l’indirizzo e-mail come identificatore univoco e limita quindi una persona a un solo CRMID, numero di telefono e/o indirizzo e-mail associato al suo account.

## Valori di identità errati o errati

In alcuni casi, valori di identità errati e non univoci vengono acquisiti nel sistema, indipendentemente dallo spazio dei nomi. Gli esempi includono:

* Spazio dei nomi IDFA con valore di identità &quot;user_null&quot;.
   * I valori di identità IDFA devono contenere 36 caratteri: 32 caratteri alfanumerici e quattro trattini.
* Spazio dei nomi del numero di telefono con valore di identità &quot;non specificato&quot;.
   * I numeri di telefono non devono contenere caratteri dell’alfabeto.

Queste identità possono causare i seguenti grafici, in cui più identificatori CRMID vengono uniti insieme all’identità &quot;bad&quot;:

![dati errati](../images/identity-settings/bad-data.png)

Con le regole di collegamento del grafico delle identità puoi configurare il CRMID come identificatore univoco per evitare la compressione del profilo indesiderata a causa di questo tipo di dati.

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico delle identità](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Servizio Identity e Real-Time Customer Profile](../identity-and-profile.md)
* [Logica di collegamento dell’identità](../features/identity-linking-logic.md)
