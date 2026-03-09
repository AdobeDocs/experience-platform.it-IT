---
title: Panoramica dell’Assistente AI (legacy) in Adobe Experience Platform
description: Scopri l’Assistente IA (legacy), le sue sfumature e i casi d’uso, e come utilizzarlo per accelerare il flusso di lavoro con Adobe Experience Platform e Real-Time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: 68c55e370cab58ce5c93359520bf4ce671282a1b
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 5%

---

# Assistente AI (legacy) in Adobe Experience Platform

>[!IMPORTANT]
>
>Questo documento si applica all’Assistente IA (legacy). Per informazioni sull&#39;Assistente IA (generazione successiva), leggere la [Guida dell&#39;interfaccia utente dell&#39;Assistente IA](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) nella [IA nella documentazione di Experience Cloud](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/home).

Per un confronto tra Assistente IA (legacy) e Assistente IA (di nuova generazione), consulta la tabella seguente:

| Area funzionale | Assistente AI (legacy) | Assistente AI (di nuova generazione) |
| --- | --- | --- |
| Esperienza utente | L’Assistente AI (legacy) è disponibile solo in un pannello nella barra a destra. | AI Assistant (Next-Gen) è disponibile sia nel pannello della barra a destra che nell’esperienza coinvolgente a schermo intero. |
| Ambito delle funzionalità | È possibile utilizzare l’Assistente AI (legacy) sia per conoscere il prodotto che per acquisire informazioni operative. | Puoi utilizzare l’Assistente all’intelligenza artificiale (di nuova generazione) per conoscere il prodotto, ottenere informazioni operative, acquisire competenze avanzate in ambito agente ed eseguire attività in più fasi. |
| Architettura della piattaforma | L’Assistente IA (legacy) non è basato sullo stack di Agent Orchestrator. | L&#39;Assistente di intelligenza artificiale (di nuova generazione) è basato su [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), che abilita l&#39;estensibilità e il coordinamento avanzato tra le funzionalità. |
| Applicazione coperta | L’Assistente IA (legacy) è un’implementazione specifica per l’applicazione. | È possibile utilizzare AI Assistant (di nuova generazione) per un’esperienza di AI Assistant unificata in tutte le applicazioni Adobe Experience Cloud. |
| Modello di accesso e autorizzazione | Modello di accesso con ambito di applicazione allineato ai limiti dei singoli prodotti. | Tutti gli utenti possono accedere ad AI Assistant (Next-Gen) e agli agenti Experience Platform associati. **Nota**: <ul><li>**Adobe Experience Manager**: l&#39;amministratore deve concedere l&#39;autorizzazione per accedere all&#39;Assistente di intelligenza artificiale (di nuova generazione) tramite [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics**: l&#39;amministratore deve concedere l&#39;autorizzazione per accedere all&#39;Assistente di intelligenza artificiale tramite [Customer Journey Analytics Access Control](https://experienceleague.adobe.com/it/docs/analytics-platform/using/technotes/access-control?lang=en). Questo consente di porre domande sulla conoscenza del prodotto e sulle informazioni sui dati. |

Il video seguente ha lo scopo di illustrare l’Assistente per l’intelligenza artificiale.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Leggi questo documento per scoprire di più sull’Assistente AI (legacy) in Adobe Experience Platform.

Assistente IA (legacy) in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente AI (legacy) per comprendere meglio la conoscenza del prodotto, risolvere i problemi o eseguire ricerche nelle informazioni e trovare informazioni operative. L’Assistente AI (legacy) supporta Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

![È stata attivata l&#39;interfaccia dell&#39;Assistente di intelligenza artificiale con la prima esperienza utente.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Prima di poter utilizzare l&#39;Assistente IA (versione precedente), devi accettare un [contratto utente](https://www.adobe.com/it/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html). Il contratto utente contiene anche il contratto beta pubblico. In questo modo è possibile utilizzare funzioni aggiuntive dell’Assistente AI (legacy) durante il rollout in capacità beta.

+++Selezionare per visualizzare l&#39;interfaccia del contratto utente

![Prima pagina del contratto utente.](./images/user-agreement-1.png)

![Ultima pagina del contratto utente.](./images/user-agreement-2.png)

+++

## Informazioni sull’Assistente AI {#understanding-ai-assistant}

L&#39;Assistente IA (legacy) risponde alle domande inviate eseguendo una query su un database e quindi traducendo i dati dal database in una risposta leggibile.

Questa rappresentazione interna dei dati sottostanti è nota anche come **[!DNL Knowledge Graph]**: un Web completo di concetti, dati e metadati per una determinata risposta.

[!DNL Knowledge Graph] è costituito da sottografi a cui si fa riferimento ogni volta che vengono inviate query:

* Informazioni operative sul cliente.
* Informazioni operative sui clienti nei vari meta-store.
* Documentazione di Experience League.

Prima di eseguire una query su Assistente IA (versione precedente) è necessario considerare due classi di domande:

### Conoscenza del prodotto {#product-knowledge}

Per conoscenza del prodotto si intendono i concetti e gli argomenti basati sulla documentazione di Experience League. Le domande relative alla conoscenza del prodotto possono essere ulteriormente specificate nei seguenti sottogruppi:

| Conoscenza del prodotto | Esempi |
| --- | --- |
| Apprendimento puntato | <ul><li>Qual è la differenza tra un&#39;identità e una chiave primaria o esterna?</li><li>Cosa sono i tipi di pubblico simili?</li></ul> |
| Rilevamento aperto | <ul><li>Come posso esportare questo set di dati?</li><li>Esistono schemi per i clienti del settore sanitario?</li></ul> |
| Risoluzione dei problemi | <ul><li>Perché non posso attivare uno schema di proprietà di Adobe per il profilo?</li><li>Perché non posso eliminare un segmento?</li></ul> |

{style="table-layout:auto"}

Guarda il video seguente per ulteriori informazioni sulle conoscenze del prodotto per l’Assistente di intelligenza artificiale (legacy):

>[!VIDEO](https://video.tv.adobe.com/v/3475938/?captions=ita&learn=on)

### Insight operativi {#operational-insights}

Le informazioni operative si riferiscono alle risposte che l’Assistente AI (Legacy) genera sugli oggetti di metadati (attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, percorsi, schemi e origini), inclusi i conteggi, le ricerche e l’impatto sulla derivazione. Non esamina alcun dato all’interno della sandbox.

* Quanti set di dati ho?
* Quanti attributi dello schema non sono mai stati utilizzati?
* Quale pubblico è stato attivato?

Puoi porre domande all’Assistente AI (legacy) sulle informazioni operative nei seguenti domini:

| Dominio | Metadati supportati | Metadati non supportati |
| --- | --- | --- |
| Attributi | <ul><li>Ricerca nome attributo</li><li>Attributo: relazione schema</li><li>Attributo: relazione set di dati</li><li>Attributo: relazione pubblico</li><li>Attributo - relazione di destinazione</li></ul> | <ul><li>Classe attributo</li><li>Audit</li><li>Stato obsoleto</li><li>Etichette</li><li>Valore memorizzato negli attributi</li></ul> |
| Tipi di pubblico | <ul><li>Conteggio del pubblico</li><li>Tipo di pubblico (in streaming o in batch)</li><li>Date di creazione/modifica</li><li>Stato attivazione</li><li>Conteggio dei profili</li><li>Pubblico duplicato</li><li>Ricerca definizione pubblico</li><li>Pubblico: relazione tra pubblico</li><li>Pubblico - relazione attributo</li><li>Pubblico: relazione tra set di dati</li><li>Pubblico - relazione destinazione</li><li>Ricerca nome</li><li>Ricerca per nome e ID | <ul><li>Sovrapposizioni del pubblico</li><li>Attivazione del pubblico</li><li>Pubblico - Relazioni con la campagna</li><li>Audit</li><li>Crea/modifica</li><li>Etichette</li><li>Tendenze di qualificazione dei profili</li></ul> |
| Flussi di dati | <ul><li>Conteggi dei flussi di dati</li><li>Stato del flusso di dati</li><li>Flusso di dati: relazione set di dati</li><li>Flusso di dati - relazione di origine</li></ul> | <ul><li>Creazione/modifica</li><li>Relazioni flusso di dati-batch</li><li>Acquisisci conteggio profili</li></ul> |
| Set di dati | <ul><li>Conteggio set di dati</li><li>Stato abilitazione profilo</li><li>Data di creazione/modifica</li><li>Set di dati: relazione schema</li><li>Set di dati: relazione pubblico</li><li>Set di dati: relazione attributo</li><li>Set di dati: relazione flusso di dati</li><li>Dimensione set di dati</li><li>Numero di righe</li><li>Ricerca nome </li><li>Ricerca per nome e ID</li></ul> | <ul><li>Audit</li><li>Creato da</li><li>Set di dati: relazione batch</li><li>Creazione/modifica del set di dati</li><li>Numero di profili</li><li>Ricerca di valori</li></ul> |
| Destinazioni | <ul><li>Conteggi di destinazione configurati</li><li>Destinazione - Relazione pubblico</li><li>Relazione attributo di destinazione</li></ul> | <ul><li>Configurazione account</li><li>Informazioni sulle credenziali dell&#39;account</li><li>Profili univoci attivati</li></ul> |
| Percorsi | <ul><li>Conteggi</li><li>Ricerca nome</li><li>Ricerca per nome e ID</li><li>Stato del percorso</li><li>Stato attivato (pubblico vs. eventi)</li><li>Date di creazione/modifica</li><li>Frequenza ricorrente</li></ul> | <ul><li>Attributi - Relazioni percorso</li><li>Audit</li><li>Creazione/modifica</li><li>Creato da</li><li>Eventi</li><li>Percorso - set di dati</li><li>Percorso - schema</li><li>Offerte</li><li>Tendenze di qualificazione dei profili</li><li>Eventi passaggio</li></ul> |
| Schemi | <ul><li>Conteggi schema</li><li>Data di creazione/modifica</li><li>Schema - relazione attributo</li><li>Schema: relazione tra set di dati</li><li>Schema: relazione pubblico</li><li>Stato abilitazione profilo</li><li>Ricerca nome</li><li>Ricerca per nome e ID</li></ul> | <ul><li>Audit</li><li>Creazione/modifica</li><li>Creato da</li><li>Gruppi di campi</li><li>Identità</li><li>Spazi dei nomi delle identità</li><li>Etichette</li><li>Numero di profili</li></ul> |
| Origini | <ul><li>Conteggi account</li><li>Stato account</li><li>Flussi di dati attivi/inattivi per ogni account</li><li>Connettore Source - relazione flusso di dati</li><li>Account Source - relazione flusso di dati</li></ul> | <ul><li>Informazioni sulle credenziali dell’account</li><li>Configurazione account</li><li>Metriche di acquisizione dei dati</li><li>Numero di profili</li><li>Source - relazioni batch</li></ul> |

{style="table-layout:auto"}

Per le domande sulle informazioni operative, le risposte potrebbero non riflettere lo stato corrente dell’interfaccia utente. I dati che supportano queste domande vengono aggiornati una volta ogni 24 ore. Ad esempio, le modifiche apportate dagli utenti in Real-Time CDP durante il giorno vengono sincronizzate con gli archivi dati di notte e quindi diventano disponibili per le domande degli utenti di mattina. Dovrai accedere a una sandbox per informazioni su dati specifici relativi agli oggetti.

Per ulteriori informazioni sulle informazioni operative di AI Assistant (legacy), guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3444040?captions=ita&learn=on&enablevpops)

### Ambito della funzione {#feature-scope}

Attualmente, l’ambito di AI Assistant (legacy) è il seguente:

* [Conoscenza del prodotto](./home.md#product-knowledge): l&#39;Assistente all&#39;intelligenza artificiale (legacy) può rispondere alle domande relative alla conoscenza del prodotto per Experience Platform, Real-Time Customer Data Platform e Adobe Journey Optimizer. Puoi anche approfondire gli argomenti della conoscenza del prodotto per Customer Journey Analytics, ma solo tramite l’interfaccia utente di Customer Journey Analytics.
* [Informazioni operative](./home.md#operational-insights): puoi chiedere all&#39;Assistente AI (legacy) domande sulle informazioni operative sui seguenti oggetti dati: attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, percorsi, schemi e origini.

## Passaggi successivi

Ora che hai una conoscenza generale di AI Assistant (Legacy), puoi procedere e utilizzare AI Assistant (Legacy) durante i flussi di lavoro. Per ulteriori informazioni, consulta la seguente documentazione:

* [Guida all’interfaccia utente di Assistente IA (legacy)](./ui-guide.md)
* [Accesso alle funzioni](./access.md)
* [Guida alle domande](./questions.md)
* [Privacy, sicurezza e governance nell’Assistente IA (legacy)](./privacy.md)
* [Domande frequenti](./faq.md)
