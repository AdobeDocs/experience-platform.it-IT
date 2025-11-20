---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;durata;ttl;durata;pseudonimo;profili pseudonimi;scadenza dati;scadenza dati;
solution: Experience Platform
title: Scadenza dati profilo pseudonimo
description: Questo documento fornisce indicazioni generali sulla configurazione della scadenza dei dati per i profili pseudonimi in Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 8734b85914d965eebc2f8ccd8c09dd1ffede8cf9
workflow-type: tm+mt
source-wordcount: '1260'
ht-degree: 7%

---

# Scadenza dei dati dei profili pseudonimi

In Adobe Experience Platform, puoi configurare i tempi di scadenza dei dati per i profili pseudonimi, consentendoti di rimuovere automaticamente dall’archivio profili i dati che non sono più validi o utili per i tuoi casi d’uso.

## Profilo pseudonimo {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="Che cos’è un profilo pseudonimo?"
>abstract="Un profilo pseudonimo è un profilo con uno spazio dei nomi delle identità pseudonimo o sconosciuto o un profilo che non ha presentato alcuna attività per un determinato periodo di tempo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Scadenza dati profilo identificato da pseudonimo"
>abstract="La scadenza dei dati del profilo pseudonimo rappresenta il numero di giorni in cui un profilo pseudonimo rimarrà in Adobe Experience Platform prima di essere rimosso. Questo valore deve essere impostato almeno su 1. Tieni presente che la rimozione del profilo pseudonimo potrebbe richiedere fino a tre giorni."

Un profilo viene considerato per la scadenza dei dati pseudonimi se soddisfa le seguenti condizioni:

- Gli spazi dei nomi delle identità del profilo unito corrispondono a quelli specificati dal cliente come spazio dei nomi di identità pseudonimo o sconosciuto.
   - Ad esempio, se lo spazio dei nomi dell&#39;identità del profilo è `ECID`, `GAID` o `AAID`. Il profilo unito non dispone di ID da altri spazi dei nomi di identità. In questo esempio, un profilo unito **non** ha un&#39;identità di posta elettronica o CRM.
- Non è stata eseguita alcuna attività in un periodo di tempo definito dall&#39;utente. L’attività è definita da qualsiasi evento esperienza acquisito o dagli aggiornamenti degli attributi del profilo avviati dal cliente.
   - Ad esempio, un nuovo evento di visualizzazione della pagina o un aggiornamento dell’attributo age è considerato un’attività. Tuttavia, un aggiornamento dell&#39;appartenenza a un pubblico non avviato dall&#39;utente è **not** considerato come un&#39;attività. Attualmente, per calcolare la scadenza dei dati, il tracciamento a livello di profilo si basa sul momento dell’evento per gli eventi esperienza e sul momento di acquisizione per gli attributi del profilo.

## Accesso {#access}

>[!AVAILABILITY]
>
>Per accedere a questa funzione, è necessario disporre delle seguenti autorizzazioni:
>
>- Gestione impostazioni profilo
>- Visualizza profili
>- Visualizzare gli spazi dei nomi delle identità
>
>L&#39;autorizzazione **Gestione impostazioni profilo** consente di impostare le scadenze dei dati, l&#39;autorizzazione **Visualizza profili** consente di visualizzare le scadenze dei dati e l&#39;autorizzazione **Visualizza spazi dei nomi delle identità** consente di visualizzare gli spazi dei nomi delle identità disponibili che è possibile utilizzare.
>
>Ulteriori informazioni sulle autorizzazioni in Experience Platform sono disponibili nella [panoramica sul controllo degli accessi](../access-control/home.md#permissions).

Per aggiungere la scadenza dei dati del profilo pseudonimo alla tua organizzazione, vai alla dashboard Profilo e seleziona **[!UICONTROL Settings]**.

![Il pulsante Impostazioni nel dashboard Profilo è evidenziato.](./images/pseudonymous-profiles/profile-settings.png)

Verrà visualizzato il popover [!UICONTROL Profile settings]. In questo popover puoi impostare il numero di giorni per la scadenza dei dati del profilo pseudonimo e lo spazio dei nomi delle identità utilizzato per la scadenza dei dati.

Per le sandbox di produzione, la scadenza predefinita dei dati del profilo pseudonimo è di 14 giorni, con un minimo di 1 giorno e un massimo di 365 giorni. Per le sandbox di sviluppo, la scadenza predefinita dei dati del profilo pseudonimo è di 3 giorni, con un minimo di 1 giorno e un massimo di 365 giorni.

Seleziona **[!UICONTROL Apply]** per salvare le impostazioni di scadenza dei dati.

![Il popover per aggiungere la scadenza dei dati del profilo pseudonimo ai profili della tua organizzazione. Il pulsante Applica è evidenziato.](./images/pseudonymous-profiles/profile-settings-data-expiry.png){width="800" zoomable="yes"}

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti relative alla scadenza dei dati dei profili pseudonimi:

### In che modo la scadenza dei dati di profilo pseudonimo differisce dalla scadenza dei dati di Experience Event?

+++ Risposta

La scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza sono funzioni complementari.

#### Granularità

La scadenza dei dati del profilo pseudonimo funziona a un livello **sandbox**. Di conseguenza, la scadenza dei dati influirà su tutti i profili nella sandbox.

La scadenza dei dati di Experience Event funziona a un livello di **set di dati**. Di conseguenza, ogni set di dati può avere un’impostazione di scadenza dati diversa.

#### Tipi di identità

Scadenza dati profilo pseudonimo **only** considera i profili con grafici di identità contenenti spazi dei nomi di identità selezionati dal cliente, ad esempio `ECID`, `AAID` o altri tipi di cookie. Se il profilo contiene **qualsiasi** spazio dei nomi di identità aggiuntivo **not** nell&#39;elenco selezionato del cliente, il profilo **not** verrà eliminato.

La scadenza dei dati dell&#39;evento esperienza rimuove gli eventi **solo** in base alla marca temporale del record evento. Gli spazi dei nomi di identità inclusi sono **ignorati** a scopo di scadenza.

#### Elementi rimossi

La scadenza dei dati del profilo pseudonimo rimuove **sia** record evento che record profilo. Di conseguenza, verranno rimossi anche i dati della classe di profilo.

La scadenza dei dati di Experience Event **only** rimuove gli eventi e **not** rimuove i dati della classe di profilo. I dati della classe profilo vengono rimossi solo quando tutti i dati vengono rimossi in **tutti** i set di dati e sono presenti **nessun** record della classe profilo rimanenti per il profilo.

+++

### In che modo la scadenza dei dati di profilo pseudonimo può essere utilizzata insieme alla scadenza dei dati di Experience Event?

+++ Risposta

Puoi utilizzare la scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza per completarsi a vicenda.

Devi **sempre** impostare la scadenza dei dati di Experience Event nei set di dati, in base alle tue esigenze di conservazione dei dati sui tuoi clienti noti. Una volta impostata la scadenza dei dati di Experience Event, puoi utilizzare la scadenza dei dati di profilo pseudonimo per rimuovere automaticamente i profili pseudonimi. In genere, il periodo di scadenza dei dati per i profili pseudonimi è inferiore al periodo di scadenza dei dati per gli eventi esperienza.

Per un caso d’uso tipico, puoi impostare la scadenza dei dati Experience Event in base ai valori dei dati utente noti e impostare la scadenza dei dati del profilo pseudonimo su una durata molto più breve per limitare l’impatto dei profili pseudonimi sulla conformità della licenza Experience Platform.

+++

### Per quali tipi di casi d’uso dovrei usare la scadenza dei dati di profili pseudonimi?

+++ Risposta

- Se utilizzi Web SDK per inviare dati direttamente ad Experience Platform.
- Se disponi di un sito web che serve in massa clienti non autenticati.
- Se nei set di dati sono presenti conteggi di profilo eccessivi e hai confermato che tali conteggi sono dovuti a uno spazio dei nomi di identità anonimo basato su cookie.
   - Per determinare ciò, è necessario utilizzare il rapporto di sovrapposizione dello spazio dei nomi delle identità. Ulteriori informazioni su questo report sono disponibili nella sezione [report di sovrapposizione identità](./api/preview-sample-status.md#identity-overlap-report) della guida dell&#39;API per l&#39;anteprima dello stato di esempio.

+++

### Quali sono alcune avvertenze di cui dovresti essere a conoscenza prima di utilizzare la scadenza dei dati dei profili pseudonimi?

+++ Risposta

- La scadenza dei dati del profilo pseudonimo viene eseguita a un livello di **sandbox**. Puoi scegliere di avere diverse configurazioni per le sandbox di produzione e di sviluppo.
- Dopo aver attivato questa funzione, l&#39;eliminazione dei profili è **permanente**. Esiste un modo **no** per eseguire il rollback o ripristinare i profili eliminati.
- Questo è **non** un processo di pulizia una tantum. La scadenza dei dati del profilo pseudonimo viene eseguita una volta al giorno ed elimina i profili che corrispondono all’input del cliente.
- **Tutti** i profili definiti come profili pseudonimi saranno interessati dalla scadenza dei dati del profilo pseudonimo. **not** ha importanza se il profilo è solo Experience Event o se contiene solo attributi di profilo.
- Questa pulizia verrà eseguita **solo** nel profilo. Identity Service può continuare a mostrare le identità eliminate all&#39;interno del grafico dopo la pulizia nei casi in cui al profilo siano associate due o più identità pseudonime (ad esempio `AAID` e `ECID`). Questa discrepanza sarà affrontata nel prossimo futuro.
- La scadenza dei dati del profilo pseudonimo **non** viene eseguita immediatamente e l&#39;elaborazione potrebbe richiedere fino a tre giorni.

+++

### In che modo la scadenza dei dati dei profili pseudonimi interagisce con i guardrail per i dati del servizio Identity?

+++ Risposta

- Il sistema di eliminazione [ del servizio Identity ](../identity-service/guardrails.md) &quot;first-in, first-out&quot; potrebbe eliminare gli ECID dal grafo delle identità, archiviati in Identity Service.
- Se questo comportamento di eliminazione determina la memorizzazione di un profilo solo ECID nel profilo cliente in tempo reale (archivio profili), la scadenza dei dati del profilo pseudonimo eliminerà tale profilo dall’archivio profili.

+++

## Passaggi successivi

Dopo aver letto questa guida, sai come visualizzare e creare le scadenze dei dati del profilo Pseudonimo. Per ulteriori informazioni sulla gestione dei dati su Experience Platform nel suo complesso, consulta la [Guida alle best practice per l&#39;adesione alla licenza di gestione dei dati](../landing/license-usage-and-guardrails/data-management-best-practices.md).

