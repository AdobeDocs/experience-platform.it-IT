---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;criteri di unione;interfaccia utente;interfaccia utente;timestamp ordinato;precedenza set di dati
title: Panoramica sui criteri di unione
type: Documentation
description: Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli per ottenere una visualizzazione completa dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare come i dati avranno priorità e quali saranno combinati per creare la vista unificata.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 1%

---

# Panoramica sui criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli in modo da ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare la priorità dei dati e i dati che verranno combinati per creare una visualizzazione unificata.

Utilizzando le API RESTful o l’interfaccia utente di, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Questo documento fornisce una panoramica dei criteri di unione e del ruolo che svolgono all’interno di Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza di diverse importanti funzionalità di [!DNL Experience Platform]. Prima di seguire questa guida e lavorare con i criteri di unione, consulta la documentazione relativa ai seguenti servizi:

* [Profilo cliente in tempo reale](../home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): abilita il profilo cliente in tempo reale collegando le identità da diverse origini dati acquisite in [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

## Informazioni sui criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli in modo da ottenere una visualizzazione completa e unificata di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare come i dati avranno priorità e quali saranno combinati per creare tale vista unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un unico profilo per quel cliente.

Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot; mentre l’altro lo elenca come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell’individuo.

I criteri di unione sono privati per la tua organizzazione e ti consentono di creare diversi criteri per unire gli schemi nei modi specifici necessari. È inoltre possibile specificare un criterio di unione predefinito che verrà utilizzato se non ne viene specificato esplicitamente uno. Per ulteriori informazioni, consulta la sezione sui [criteri di unione predefiniti](#default-merge-policy) più avanti in questo documento. È consentito un massimo di cinque criteri di unione per organizzazione.

## Metodi di unione {#merge-methods}

Ogni frammento di profilo contiene informazioni relative a una sola identità sul numero totale di identità che potrebbero esistere per un singolo utente. Quando unisci tali dati per formare un profilo cliente, esiste la possibilità che tali informazioni entrino in conflitto ed è necessario specificare la priorità.

La selezione di un metodo di unione consente di specificare gli attributi del set di dati da assegnare come priorità se si verifica un conflitto di unione tra i set di dati.

Sono disponibili due possibili metodi di unione per i criteri di unione. Ciascuno di questi metodi è riassunto di seguito con informazioni aggiuntive fornite nelle sezioni che seguono:

* **[!UICONTROL Precedenza set di dati]:** In caso di conflitto, assegna priorità ai frammenti di profilo in base al set di dati da cui provengono. Quando selezioni questa opzione, devi scegliere i set di dati correlati e il loro ordine di priorità. Ulteriori informazioni sul metodo di unione [precedenza set di dati](#dataset-precedence).
* **[!UICONTROL Timestamp ordinato]:** In caso di conflitto, viene data priorità al frammento di profilo aggiornato più di recente. Ulteriori informazioni sul metodo di unione [timestamp ordinato](#timestamp-ordered).

### Precedenza set di dati {#dataset-precedence}

Quando **[!UICONTROL Precedenza set di dati]** è selezionato come metodo di unione per un criterio di unione, è possibile assegnare la priorità ai frammenti di profilo in base al set di dati da cui provengono. Un caso d’uso esemplificativo è quello in cui l’organizzazione disponeva di informazioni presenti in un set di dati preferito o attendibili rispetto ai dati di un altro set di dati.

Per creare un criterio di unione utilizzando **[!UICONTROL Precedenza set di dati]**, è necessario selezionare i set di dati Profilo e ExperienceEvent inclusi e quindi ordinare manualmente i set di dati Profilo per la precedenza. Una volta selezionati e ordinati i set di dati, al set di dati superiore verrà assegnata la priorità più alta, al secondo il set di dati più alto e così via.

### Timestamp ordinato {#timestamp-ordered}

Quando i record di profilo vengono acquisiti in Experience Platform, al momento dell’acquisizione viene ottenuta una marca temporale di sistema che viene aggiunta al record. Quando **[!UICONTROL Timestamp ordinato]** è selezionato come metodo di unione per un criterio di unione, i profili vengono uniti in base alla marca temporale del sistema. In altre parole, l’unione viene eseguita in base alla marca temporale di quando il record è stato acquisito in Platform.

## Unione identità {#id-stitching}

L&#39;unione di identità ([!UICONTROL unione ID]) è il processo di identificazione dei frammenti di dati e di loro combinazione per formare un record di profilo completo. Per illustrare i diversi comportamenti di unione, considera un singolo cliente che interagisce con un brand utilizzando due indirizzi e-mail diversi.

* **[!UICONTROL Nessuno]:** Quando questa opzione è selezionata, gli ID non verranno uniti. Quando si verifica la segmentazione, le identità che possono appartenere alla stessa persona non vengono unite tra loro e la segmentazione prenderà in considerazione solo gli attributi associati a ogni singolo ID nel determinare se un cliente si qualifica per l’iscrizione al pubblico. Questo poteva comportare che un singolo cliente avesse più profili e che ogni profilo potesse qualificarsi per diversi tipi di pubblico, con conseguente invio di più messaggi di marketing allo stesso cliente.
* **[!UICONTROL Grafo privato]:** Quando il grafo privato è selezionato, più identità relative allo stesso individuo sono unite insieme. Questo comporta che il cliente abbia un singolo profilo e consente alla segmentazione di considerare più attributi da più identità correlate durante la determinazione della qualifica del segmento. In questo scenario, è probabile che il cliente abbia un singolo profilo, si qualifichi per un pubblico in base alla combinazione di attributi tra identità e riceva un solo messaggio di marketing.

Per ulteriori informazioni sulle identità e sul loro ruolo nella generazione di profili e tipi di pubblico, consulta la [panoramica del servizio Identity](../../identity-service/home.md).

## Criterio di unione predefinito {#default-merge-policy}

Un’organizzazione può creare un criterio di unione predefinito da utilizzare per l’unione di frammenti di profilo. Questo consente agli utenti di selezionare facilmente il criterio predefinito durante l’esecuzione di azioni come la visualizzazione dei profili dei clienti o la creazione di tipi di pubblico, in Experience Platform. Nella maggior parte dei casi, a meno che non venga specificato un altro criterio di unione, verrà utilizzato quello predefinito.

Ogni organizzazione può creare più criteri di unione correlati a una singola classe di schema XDM, ma è possibile dichiarare un solo criterio di unione predefinito per ogni classe. Ad esempio, l&#39;organizzazione potrebbe disporre di un criterio di unione predefinito correlato alla classe [!DNL XDM Individual Profile] e di un criterio di unione predefinito diverso per una classe Product Inventory personalizzata.

Se si crea un nuovo criterio di unione e lo si imposta come predefinito, il criterio di unione predefinito precedente verrà aggiornato automaticamente dal sistema in modo da non essere più quello predefinito.

>[!WARNING]
>
>Potrebbero essere interessati i conteggi dei profili e i tipi di pubblico associati a un criterio di unione predefinito esistente. Qualsiasi pubblico a cui è applicato un criterio di unione predefinito verrà aggiornato al nuovo criterio di unione predefinito.

## Passaggi successivi

Dopo aver letto questa guida, saprai cosa sono i criteri di unione e il ruolo che svolgono all’interno di Experience Platform. Per iniziare a utilizzare i criteri di unione nell&#39;interfaccia utente di Experience Platform, consulta la [guida dell&#39;interfaccia utente dei criteri di unione](ui-guide.md). Per utilizzare i criteri di unione tramite API, visita la [guida dell&#39;endpoint API per i criteri di unione](../api/merge-policies.md).
