---
keywords: Experience Platform; casa; argomenti popolari; Dataset; Dataset; tempo per vivere; Ttl; tempo di vita; pseudonimo; profili pseudonimi; scadenza dei dati; scadenza;
solution: Experience Platform
title: Pseudonimo Scadenza dei dati del profilo
description: In questo documento vengono fornite indicazioni generali sulla configurazione della scadenza dei dati per profili pseudonimi all'interno di Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 6%

---

# Scadenza dei dati dei profili pseudonimi

In Adobe Experience Platform, è possibile configurare i tempi di scadenza dei dati per i profili pseudonimi, consentendo di rimuovere automaticamente dalla store del profilo i dati che non sono più validi o utili per i casi d&#39;uso.

## Profilo pseudonimo {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="Che cos’è un profilo pseudonimo?"
>abstract="Un profilo pseudonimo è un profilo con uno spazio dei nomi di identità pseudonimo o sconosciuto o un profilo che non ha presentato alcuna attività per un determinato periodo di tempo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Scadenza dei dati del profilo pseudonimo"
>abstract="La scadenza dei dati di un profilo pseudonimo rappresenta il numero di giorni in cui un profilo pseudonimo rimarrà in Adobe Experience Platform prima di essere rimosso."

Un profilo viene considerato per la scadenza dei dati pseudonimi se soddisfa le seguenti condizioni:

- Gli spazi dei nomi delle identità del profilo unito corrispondono a quelli specificati dal cliente come spazio dei nomi di identità pseudonimo o sconosciuto.
   - Ad esempio, se lo spazio dei nomi dell&#39;identità del profilo è `ECID`, `GAID` o `AAID`. Il profilo unito non dispone di ID da altri spazi dei nomi di identità. In questo esempio, un profilo unito **non** ha un&#39;identità di posta elettronica o CRM.
- Non è stata eseguita alcuna attività in un periodo di tempo definito dall&#39;utente. L’attività è definita da qualsiasi evento esperienza acquisito o dagli aggiornamenti degli attributi del profilo avviati dal cliente.
   - Ad esempio, un nuovo evento di visualizzazione della pagina o un aggiornamento dell’attributo age è considerato un’attività. Tuttavia, un aggiornamento dell&#39;appartenenza a un pubblico non avviato dall&#39;utente è **not** considerato come un&#39;attività. Attualmente, per calcolare la scadenza dei dati, il tracciamento a livello di profilo si basa sul momento dell’evento per gli eventi esperienza e sul momento di acquisizione per gli attributi del profilo.

## Accesso {#access}

La scadenza dei dati del profilo pseudonimo non può essere configurata tramite l’interfaccia utente o le API di Experience Platform. Per abilitare questa funzione, è necessario contattare il supporto tecnico. Quando si contatta l’assistenza, includere le seguenti informazioni:

- Gli spazi dei nomi delle identità da considerare per le eliminazioni di profili pseudonimi.
   - Ad esempio: `ECID` solo, `AAID` solo o una combinazione di `ECID` e `AAID`.
- Il tempo di attesa prima di eliminare un profilo con un nome di pseudonimo. Il consiglio predefinito per i clienti è 14 giorni. Tuttavia, questo valore può variare in base al caso d&#39;uso.

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande più frequenti relative alla scadenza dei dati dei profili pseudonimi:

### In che modo la scadenza dei dati del profilo pseudonimo differisce dalla scadenza dei dati degli eventi esperienza?

Pseudonimo La scadenza dei dati del profilo e la scadenza dei dati degli eventi dell&#39;esperienza sono funzioni complementari.

#### Granularità

Pseudonimo La scadenza dei dati del profilo funziona a **livello sandbox** . Di conseguenza, la scadenza dei dati interesserà tutti i profili nella sandbox.

La scadenza dei dati degli eventi esperienza funziona a **livello di set di dati** . Di conseguenza, ogni set di dati può avere un&#39;impostazione di scadenza dei dati diversa.

#### Tipi di identità

Scadenza dati profilo pseudonimo **only** considera i profili con grafici di identità contenenti spazi dei nomi di identità selezionati dal cliente, ad esempio `ECID`, `AAID` o altri tipi di cookie. Se il profilo contiene **qualsiasi** spazio dei nomi di identità aggiuntivo **not** nell&#39;elenco selezionato del cliente, il profilo **not** verrà eliminato.

La scadenza dei dati dell&#39;evento esperienza rimuove gli eventi **solo** in base alla marca temporale del record evento. Gli spazi dei nomi di identità inclusi sono **ignorati** a scopo di scadenza.

#### Elementi rimossi

La scadenza dei dati del profilo pseudonimo rimuove **sia** record evento che record profilo. Di conseguenza, verranno rimossi anche i dati della classe di profilo.

La scadenza dei dati di Experience Event **only** rimuove gli eventi e **not** rimuove i dati della classe di profilo. I dati della classe profilo vengono rimossi solo quando tutti i dati vengono rimossi in **tutti** i set di dati e sono presenti **nessun** record della classe profilo rimanenti per il profilo.

### In che modo la scadenza dei dati di profilo pseudonimo può essere utilizzata insieme alla scadenza dei dati di Experience Event?

Puoi utilizzare la scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza per completarsi a vicenda.

Devi **sempre** impostare la scadenza dei dati di Experience Event nei set di dati, in base alle tue esigenze di conservazione dei dati sui tuoi clienti noti. Una volta impostata la scadenza dei dati degli eventi esperienza, puoi utilizzare la scadenza dei dati del profilo pseudonimo per rimuovere automaticamente i profili pseudonimi. In genere, il periodo di scadenza dei dati per i profili pseudonimi è inferiore al periodo di scadenza dei dati per gli eventi esperienza.

Per un caso d&#39;uso tipico, puoi impostare la scadenza dei dati dell&#39;Evento esperienza in base ai valori dei tuoi dati utente noti e impostare la scadenza dei dati del tuo profilo pseudonimo a una durata molto più breve per limitare l&#39;impatto dei profili pseudonimi sulla conformità della licenza Experience Platform.

### Quali utenti dovrebbero utilizzare la scadenza dei dati dei profili pseudonimi?

- Se utilizzi Web SDK per inviare direttamente dati a Experience Platform.
- Se disponi di un sito web che serve in massa clienti non autenticati.
- Se nei set di dati sono presenti conteggi di profili eccessivi e si è verificato che questo numero eccessivo di profili è dovuto allo spazio dei nomi identità anonimo basato su cookie.
   - Per determinare ciò, è necessario utilizzare il rapporto di sovrapposizione dello spazio dei nomi delle identità. Ulteriori informazioni su questo report sono disponibili nella sezione [report di sovrapposizione identità](./api/preview-sample-status.md#identity-overlap-report) della guida dell&#39;API per l&#39;anteprima dello stato di esempio.

### Quali sono alcune avvertenze di cui dovresti essere a conoscenza prima di utilizzare la scadenza dei dati dei profili pseudonimi?

- La scadenza dei dati del profilo pseudonimo viene eseguita a un livello di **sandbox**. Puoi scegliere di avere diverse configurazioni per le sandbox di produzione e di sviluppo.
- Dopo aver attivato questa funzione, l&#39;eliminazione dei profili è **permanente**. Esiste un modo **no** per eseguire il rollback o ripristinare i profili eliminati.
- Questo è **non** un processo di pulizia una tantum. La scadenza dei dati del profilo pseudonimo viene eseguita una volta al giorno ed elimina i profili che corrispondono all’input del cliente.
- **Tutti** i profili definiti come profili pseudonimi saranno interessati dalla scadenza dei dati del profilo pseudonimo. **not** ha importanza se il profilo è solo Experience Event o se contiene solo attributi di profilo.
- Questa pulizia verrà eseguita **solo** nel profilo. Identity Service può continuare a mostrare le identità eliminate all&#39;interno del grafico dopo la pulizia nei casi in cui al profilo siano associate due o più identità pseudonime (ad esempio `AAID` e `ECID`). Questa discrepanza sarà affrontata nel prossimo futuro.
- La scadenza dei dati del profilo con pseudonimi non **viene** eseguita immediatamente e l&#39;elaborazione può richiedere fino a tre giorni.

### In che modo la scadenza dei dati dei profili pseudonimi interagisce con i guardrail per i dati del servizio Identity?

- Il sistema](../identity-service/guardrails.md) di eliminazione &quot;first-in, first-out&quot; di Identity Service [potrebbe eliminare gli ECID dal grafico delle identità, che sono memorizzati in Identity Service.
- Se questo comportamento di eliminazione comporta la memorizzazione di un profilo solo ECID nel profilo cliente in tempo reale (store profilo), la scadenza dei dati del profilo pseudonimo eliminerà il profilo dalla store del profilo.
