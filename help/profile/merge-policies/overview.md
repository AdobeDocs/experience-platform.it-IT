---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;criteri di unione;interfaccia utente;interfaccia utente;timestamp ordinato;precedenza set di dati
title: Panoramica dei criteri di unione
type: Documentation
description: Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visione completa dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare la visualizzazione unificata.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 965993bece32eeb0db6e7a9eab3131816a9de5cd
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Panoramica sui criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si uniscono questi dati, i criteri di unione sono regole che [!DNL Platform] utilizza per determinare come assegnare una priorità ai dati e quali saranno i dati combinati per creare una visualizzazione unificata.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Questo documento fornisce una panoramica dei criteri di unione e del ruolo che essi svolgono all&#39;interno dell&#39;Experience Platform.

## Introduzione

Questa guida richiede una comprensione operativa di diverse importanti [!DNL Experience Platform] funzionalità. Prima di seguire questa guida e di utilizzare i criteri di unione, controlla la documentazione relativa ai seguenti servizi:

* [Profilo cliente in tempo reale](../home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): Abilita il profilo del cliente in tempo reale collegando le identità da diverse origini dati in cui viene effettuato l’acquisizione [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

## Informazioni sui criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa e unificata di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare tale visualizzazione unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente.

Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l’altro elenca il cliente come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell’utente.

I criteri di unione sono privati dell’organizzazione e consentono di creare diversi criteri per unire gli schemi nei modi specifici necessari. È inoltre possibile specificare un criterio di unione predefinito che verrà utilizzato se non viene fornito in modo esplicito. Vedi la sezione su [criteri di unione predefiniti](#default-merge-policy) più avanti in questo documento per ulteriori informazioni. È consentito un massimo di cinque criteri di unione per organizzazione.

## Metodi di unione {#merge-methods}

Ogni frammento di profilo contiene informazioni per una sola identità sul numero totale di identità che possono esistere per un singolo utente. Quando unisci i dati per formare un profilo cliente, è possibile che tali informazioni siano in conflitto e occorre specificare la priorità.

La selezione di un metodo di unione consente di specificare quali attributi del set di dati dare la priorità se si verifica un conflitto di unione tra i set di dati.

Sono disponibili due possibili metodi di unione per i criteri di unione. Ciascuno di questi metodi è riassunto di seguito con ulteriori dettagli forniti nelle sezioni seguenti:

* **[!UICONTROL Precedenza del set di dati]:** In caso di conflitto, assegna priorità ai frammenti di profilo in base al set di dati da cui provengono. Quando selezioni questa opzione, devi scegliere i set di dati correlati e il loro ordine di priorità. Ulteriori informazioni sulle [precedenza del set di dati](#dataset-precedence) metodo merge.
* **[!UICONTROL Timestamp ordinato]:** In caso di conflitto, viene data priorità al frammento di profilo aggiornato più di recente. Ulteriori informazioni sulle [timestamp ordinato](#timestamp-ordered) metodo merge.

### Precedenza del set di dati {#dataset-precedence}

Quando **[!UICONTROL Precedenza del set di dati]** è selezionato come metodo di unione per un criterio di unione, è possibile assegnare la priorità ai frammenti di profilo in base al set di dati da cui provengono. Un esempio di caso d’uso è quello di informazioni presenti in un set di dati preferito o attendibile rispetto ai dati di un altro set di dati.

Per creare un criterio di unione utilizzando **[!UICONTROL Precedenza del set di dati]**, devi selezionare i set di dati Profilo ed ExperienceEvent inclusi e quindi puoi ordinare manualmente i set di dati Profilo per la precedenza. Una volta selezionati e ordinati i set di dati, al set di dati principale verrà data la priorità più alta, al secondo e così via.

### Timestamp ordinato {#timestamp-ordered}

Poiché i record di profilo vengono acquisiti in Experience Platform, al momento dell’acquisizione viene ottenuta una marca temporale di sistema che viene aggiunta al record. Quando **[!UICONTROL Timestamp ordinato]** è selezionato come metodo di unione per un criterio di unione, i profili vengono uniti in base alla marca temporale del sistema. In altre parole, l’unione viene eseguita in base alla marca temporale per quando il record è stato acquisito in Platform.

## Unione identità {#id-stitching}

Unione identità ([!UICONTROL unione degli ID]) è il processo di identificazione dei frammenti di dati e di loro combinazione per formare un record completo del profilo. Per illustrare i diversi comportamenti di unione, considera un singolo cliente che interagisce con un marchio utilizzando due indirizzi e-mail diversi.

* **[!UICONTROL Nessuno]:** Quando questa opzione è selezionata, gli ID non vengono uniti. Quando si verifica la segmentazione, le identità che possono appartenere alla stessa persona non vengono unite e la segmentazione considera solo gli attributi associati a ciascun singolo ID quando si determina se un cliente è idoneo per l’appartenenza al segmento. Questo potrebbe comportare l’invio di più messaggi di marketing allo stesso cliente a un singolo cliente con più profili e ciascun profilo potrebbe qualificarsi per segmenti diversi.
* **[!UICONTROL Grafico privato]:** Quando il grafico privato è selezionato, più identità correlate allo stesso individuo vengono unite. Questo fa sì che il cliente abbia un singolo profilo e consenta alla segmentazione di considerare più attributi da più identità correlate durante la determinazione della qualifica del segmento. In questo scenario, è probabile che il cliente abbia un singolo profilo, si qualifichi per un segmento in base alla combinazione di attributi tra identità e riceva un solo messaggio di marketing.

Per ulteriori informazioni sulle identità e sul loro ruolo nella generazione di profili e segmenti, si prega di iniziare leggendo il [Panoramica del servizio Identity](../../identity-service/home.md).

## Criterio di unione predefinito {#default-merge-policy}

Un&#39;organizzazione può creare un criterio di unione predefinito da utilizzare per l&#39;unione dei frammenti di profilo. Questo consente agli utenti di selezionare facilmente il criterio predefinito durante l’esecuzione di azioni, ad Experience Platform la visualizzazione dei profili dei clienti o la creazione di segmenti. Nella maggior parte dei casi, a meno che non venga specificato un altro criterio di unione, verrà utilizzato il criterio di unione predefinito.

Ciascuna organizzazione può creare più criteri di unione relativi a una singola classe di schema XDM, tuttavia può avere un solo criterio di unione predefinito dichiarato per ogni classe. Ad esempio, l&#39;organizzazione potrebbe disporre di un criterio di unione predefinito correlato al [!DNL XDM Individual Profile] Classe e un diverso criterio di unione predefinito per una classe di Product Inventory personalizzata.

Se si crea un nuovo criterio di unione e lo si imposta come predefinito, il precedente criterio di unione predefinito verrà aggiornato automaticamente dal sistema in modo che non sia più il predefinito.

>[!WARNING]
>
>Potrebbero essere interessati i conteggi e i segmenti di profilo con un criterio di unione predefinito esistente. Tutti i segmenti a cui è stato applicato un criterio di unione predefinito verranno aggiornati al nuovo criterio di unione predefinito.

## Passaggi successivi

Dopo aver letto questa guida è ora possibile sapere cosa sono i criteri di unione e il ruolo che svolgono all’interno di Experience Platform. Per iniziare a utilizzare i criteri di unione nell’interfaccia utente di Experience Platform, consulta [guida all’interfaccia utente per i criteri di unione](ui-guide.md). Per utilizzare i criteri di unione utilizzando l’API, visita [guida all’endpoint API per i criteri di unione](../api/merge-policies.md).
