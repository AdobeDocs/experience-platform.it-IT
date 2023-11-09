---
title: Packaging servizio query
description: Il documento seguente illustra il pacchetto di funzionalità e prodotti disponibili per Query Service ed evidenzia le differenze tra query ad hoc e batch.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 2%

---

# Pacchetto Query Service

Questo documento illustra i diversi tipi di funzionalità di creazione pacchetti e di esecuzione delle query disponibili in Query Service.

Adobe Experience Platform Query Service può essere diviso in due funzionalità in base ai modelli di query che possono essere eseguiti:

- **Query ad hoc** sono query SQL utilizzate per esplorare i set di dati acquisiti per la verifica, la convalida, la sperimentazione e così via. Queste query non riscrivono i dati nel data lake di Platform.
- **Query batch** sono query SQL utilizzate per eseguire l’elaborazione post-acquisizione dei set di dati acquisiti. Queste query puliscono, modellano, manipolano e arricchiscono i dati, i cui risultati vengono riscritti nel data lake di Platform. Queste query possono essere pianificate, gestite e monitorate come processi batch.

Le funzionalità di Query Service sono fornite con i seguenti prodotti e componenti aggiuntivi:

- **Applicazioni basate su piattaforma** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics e Adobe Journey Optimizer): l’accesso a Query Service per eseguire query ad hoc viene fornito sin dall’inizio con ogni variante e livello di applicazioni basate su Platform.
- **[!DNL Data Distiller]** (pacchetto del componente aggiuntivo che può essere acquistato con Adobe Real-Time CDP, Customer Journey Analytics e Adobe Journey Optimizer): l’accesso a Query Service per eseguire query batch è fornito con [!DNL Data Distiller].

## Terminologia {#terminology}

La sezione seguente fornisce le definizioni dei termini chiave relativi alla creazione di pacchetti di Query Service:

- **Archiviazione del data lake**: il data lake ha principalmente i seguenti scopi:
   - funge da area di gestione temporanea per l’onboarding dei dati in Experienci Platform;
   - funge da archiviazione dei dati a lungo termine per tutti i dati Experienci Platform;
   - Abilita casi d’uso come analisi dei dati e data science.
- **Esportazione dati**: Il [set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=it) tipi che è possibile esportare in base all&#39;applicazione, al livello di prodotto ed eventuali componenti aggiuntivi acquistati. I set di dati derivati possono essere creati tramite il componente aggiuntivo Distiller dati di Query Service e possono essere [esportato da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activation-overview.html) per un&#39;ampia gamma di destinazioni, tra cui [destinazioni archiviazione cloud](/help/destinations/ui/export-datasets.md).
- **Query accelerate**: le query accelerate restituiscono risultati basati su dati aggregati per ridurre il tempo di attesa dei risultati e consentire uno scambio di informazioni più interattivo. Le query senza stato eseguite nell’archivio accelerato sono disponibili solo come parte del componente aggiuntivo Data Distiller.
- **Calcola ore**: le ore di calcolo sono la metrica utilizzata per monitorare la scansione e la scrittura di dati con query batch utilizzando l’API Query Service. Viene calcolato in ore all’anno e misurato in tutte le sandbox. Il numero di ore di calcolo fornite alla tua organizzazione è definito nel processo di definizione dell’ambito dell’offerta.

## Diritti {#entitlements}

La tabella seguente illustra i principali diritti di Query Service in base al modo in cui vengono inclusi nel pacchetto:

| Autenticazione servizio query | Pacchetto di applicazioni basate su piattaforma | Confezionato con [!DNL Data Distiller] |
|---|---|---|
| Pattern di query supportato | Solo query ad hoc | Query batch |
| Caso d’uso supportato | <ul><li>Esplorazione&#x200B;</li><li>Individuazione dati&#x200B;</li><li>Convalida dei dati</li><li>Sperimentazione</li></ul> | <ul><li>Pulizia</li><li>Forma</li><li>Manipolazione</li><li>Arricchimento</li></ul> |
| Semantica supportata | <ul><li>QUERY SELECT</li></ul> | <ul><li>Query CTAS e ITAS</li></ul> |
| Tempo massimo di esecuzione | 10 minuti | 24 ore |
| Metrica di licenza | **Concorrenza utente query**: <ul><li>1 utente simultaneo (Real-Time CDP, Adobe Journey Optimizer)&#x200B;</li><li>5 utenti simultanei (Customer Journey Analytics)&#x200B;</li></ul> **Concorrenza query**: <ul><li>1 query in esecuzione simultanea (tutte le applicazioni)&#x200B;</li></ul> **Componente aggiuntivo per pacchetti di utenti di query ad hoc aggiuntivi** può essere acquistato per aumentare i diritti alle query ad hoc autorizzati dai clienti. <ul><li>+5 utenti simultanei aggiuntivi per pacchetto</li><li>+1 query concorrente aggiuntiva in esecuzione per pacchetto</li></ul> | **Calcola ore**: <ul><li>Variabile (con ambito in base alle adesioni dell’applicazione del cliente)</li></ul> **Calcola ore** è una misura del tempo impiegato dal motore di Query Service per leggere, elaborare e riscrivere i dati nel data lake quando viene eseguita una query batch. |
| Utilizzo accelerato di query e reporting | No | Sì: le query accelerate simultanee consentono di leggere i dati dall’archivio e visualizzare rapidamente all’interno delle dashboard. Viene inoltre fornito un diritto dedicato per la memorizzazione di modelli di reporting e set di dati nel negozio accelerato. |
| Capacità di archiviazione del data lake | Sì - Il diritto totale allo storage dipende dalle licenze delle applicazioni basate su piattaforma. Ad esempio, Real-Time CDP, AJO, CJA e così via. | Sì: viene fornita un’ulteriore autorizzazione alla memorizzazione per mantenere i set di dati non elaborati e derivati per i casi di utilizzo di Data Distiller oltre una data di scadenza dei dati di sette giorni.<br>La capacità di archiviazione del data lake viene misurata in terabyte (TB) e dipende dalla quantità di ore di calcolo acquistate. |
| Tolleranza esportazione dati | Sì - Il diritto totale all&#39;esportazione dipende dalle licenze delle applicazioni basate su piattaforma. Ad esempio, Real-Time CDP, AJO, CJA e così via. | Sì - Vengono forniti ulteriori diritti di esportazione per consentire l’esportazione di set di dati derivati creati utilizzando Data Distiller.<br>Il limite di esportazione dei dati annuale viene misurato in terabyte (TB) e dipende dalla quantità di ore di calcolo acquistate. |
| Interfaccia di esecuzione query | <ul><li>Interfaccia utente di Query Service</li><li>Interfaccia utente client di terze parti</li><li>[!DNL PostgresSQL] interfaccia utente client</li></ul> | <ul><li>Interfaccia utente di Query Service </li><li>Interfaccia utente client di terze parti</li><li>[!DNL PostgresSQL] interfaccia utente client</li><li>API REST</li></ul> |
| Risultati Query Restituiti Tramite | Interfaccia utente client | Set di dati derivati archiviato nel data lake |
| Limite risultati | <ul><li>Interfaccia utente di Query Service - 100 righe</li><li>Clienti di terze parti - 50.000</li><li>[!DNL PostgresSQL] client - 50.000</li></ul> | <ul><li>Interfaccia utente di Query Service: il numero di righe di output può essere [configurato con un’impostazione dell’interfaccia utente](./ui/user-guide.md#result-count) tra 50 e 500 righe.</li><li>Client di terze parti (nessun limite superiore alle righe)</li><li>[!DNL PostgresSQL] client (nessun limite superiore alle righe)</li><li>API REST (nessun limite superiore alle righe)</li></ul> |
| Capacità set di dati di lettura | Sì | Sì |
| Capacità del set di dati di scrittura | No | Sì |
| Capacità di programmazione | No | Sì |
| Capacità di monitoraggio | Sì | Sì |
| Capacità impostazione avvisi query | No | Sì |

{style="table-layout:auto"}

## Controllo degli accessi {#access-control}

Ad Experience Platform, il controllo degli accessi viene gestito tramite [Adobe Admin Console](https://adminconsole.adobe.com/) i profili di prodotto collegano gli utenti con autorizzazioni e sandbox. Consulta la [panoramica sul controllo degli accessi](../access-control/home.md) per ulteriori informazioni.

Per utilizzare Query Service, è necessario [!DNL Manage Queries] l&#39;autorizzazione deve essere abilitata in Admin Console. Questa autorizzazione consente agli utenti di eseguire query ad hoc e batch. Istruzioni dettagliate per la richiesta di accesso al profilo di prodotto [!DNL Manage Queries] dell&#39;autorizzazione sono descritti nel [gestire le autorizzazioni per un profilo di prodotto](../access-control/ui/permissions.md) e [gestire gli utenti per un profilo di prodotto](../access-control/ui/users.md) documenti.

Dopo aver acquistato il [!DNL Data Distiller] componente aggiuntivo, [!DNL Write Dataset] deve essere concessa l’autorizzazione. Questa autorizzazione consente [!DNL Data Distiller] utenti per eseguire query batch.

La tabella seguente illustra gli effetti della [!DNL Manage Queries] autorizzazione:

| Autorizzazione | Funzione |
|---|---|
| [!DNL Manage Queries] (senza autorizzazione per la scrittura dei dati) | Consente di accedere per eseguire query ad hoc |
| [!DNL Manage Queries] (con autorizzazione per la scrittura dei dati) | Fornisce l’accesso per eseguire query batch |

{style="table-layout:auto"}

## Supporto sandbox {#sandbox-support}

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experienci Platform. Ogni istanza di Platform supporta più sandbox di produzione e non di produzione, ognuna delle quali mantiene la propria libreria di risorse Platform. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulle sandbox di produzione. Per ulteriori informazioni sulle sandbox, consulta [panoramica sulle sandbox](../sandboxes/home.md). Tutti i diritti di Query Service sono condivisi tra tutte le sandbox.

## Passaggi successivi

Una volta letto questo documento, sarai in grado di comprendere meglio i diversi tipi di pacchetti e le diverse funzionalità di esecuzione delle query disponibili in Query Service. Per ulteriori informazioni su Query Service, ad esempio sui casi d’uso noti nel settore, consulta [documentazione del caso d’uso](./use-cases/abandoned-browse.md). Per informazioni più generali, visitare il [Panoramica di Query Service](./home.md).
