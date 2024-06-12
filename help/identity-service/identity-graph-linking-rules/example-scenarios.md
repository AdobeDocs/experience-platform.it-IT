---
title: Scenari Di Esempio Per La Configurazione Delle Impostazioni Delle Identità
description: Scopri alcuni scenari di esempio per la configurazione delle impostazioni delle identità.
badge: Beta
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: f1779ee75c877649a69f9fa99f3872aea861beca
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# Scenari di esempio per la configurazione delle regole di collegamento del grafico delle identità

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

![shared-devices](../images/identity-settings/shared-devices.png)

In questi casi, dal punto di vista del grafico, senza limiti abilitati, un singolo ECID sarà collegato a più ID del sistema di gestione delle relazioni con i clienti.

Con le regole di collegamento del grafico delle identità, puoi:

* Configura l’ID utilizzato per l’accesso come identificatore univoco. Ad esempio, puoi limitare un grafico per memorizzare una sola identità con un ID del sistema di gestione delle relazioni con i clienti spazio dei nomi, e quindi definire tale ID del sistema di gestione delle relazioni con i clienti come identificatore univoco di un dispositivo condiviso.
   * In questo modo, puoi evitare che gli ID del sistema di gestione delle relazioni con i clienti vengano uniti dall’ECID.

## Scenari e-mail/telefono non validi

Ci sono anche esempi di utenti che forniscono valori falsi come numeri di telefono e/o indirizzi e-mail al momento della registrazione. In questi casi, se i limiti non sono abilitati, le identità relative a telefono/e-mail finiranno per essere collegate a più ID CRM diversi.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Con le regole di collegamento del grafico delle identità, puoi:

* Configura l’ID del sistema di gestione delle relazioni con i clienti, il numero di telefono o l’indirizzo e-mail come identificatore univoco e limita quindi una persona a un solo ID del sistema di gestione delle relazioni con i clienti, numero di telefono e/o indirizzo e-mail associato al suo account.

## Valori di identità errati o errati

In alcuni casi, valori di identità errati e non univoci vengono acquisiti nel sistema, indipendentemente dallo spazio dei nomi. Gli esempi includono:

* Spazio dei nomi IDFA con valore di identità &quot;user_null&quot;.
   * I valori di identità IDFA devono contenere 36 caratteri: 32 caratteri alfanumerici e quattro trattini.
* Spazio dei nomi del numero di telefono con valore di identità &quot;non specificato&quot;.
   * I numeri di telefono non devono contenere caratteri dell’alfabeto.

Queste identità possono causare i seguenti grafici, in cui più ID del sistema di gestione delle relazioni con i clienti vengono uniti insieme all’identità &quot;errata&quot;:

![bad-data](../images/identity-settings/bad-data.png)

Con le regole di collegamento del grafico delle identità puoi configurare l’ID del sistema di gestione delle relazioni con i clienti come identificatore univoco per evitare la compressione del profilo indesiderata dovuta a questo tipo di dati.

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico delle identità](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Servizio Identity e Real-Time Customer Profile](../identity-and-profile.md)
* [Logica di collegamento dell’identità](../features/identity-linking-logic.md)
