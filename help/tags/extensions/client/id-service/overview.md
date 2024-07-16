---
title: Panoramica dell’estensione Adobe Experience Cloud Identity Service
description: Scopri l’estensione tag Adobe Experience Cloud Identity Service in Adobe Experience Platform.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 97%

---

# Panoramica dell’estensione Adobe Experience Cloud Identity Service

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Usa questa guida di riferimento per informazioni sulla configurazione dell’estensione Adobe Experience Cloud ID e sulle opzioni disponibili quando utilizzi questa estensione per generare una regola.

Usa questa estensione per integrare Experience Cloud Identity Service nella tua proprietà. Con Experience Cloud Identity Service, puoi creare e memorizzare identificatori univoci e costanti per i visitatori del tuo sito.

## Configurare l&#39;estensione Experience Cloud ID

Questa sezione fornisce un riferimento sulle opzioni disponibili durante la configurazione dell&#39;estensione Experience Cloud ID.

Se l’estensione Experience Cloud ID non è ancora stata installata, apri la proprietà, quindi fai clic su **[!UICONTROL Estensioni > Catalogo]**, passa il puntatore sull’estensione Experience Cloud ID e fai clic su **[!UICONTROL Installa]**.

Per configurare l’estensione, apri la scheda Estensioni, passa il puntatore sull’estensione e fai clic su **[!UICONTROL Configura]**.

![](../../../images/optin.jpg)

Sono disponibili le seguenti configurazioni:

### ID organizzazione Experience Cloud

L&#39;ID per Experience Cloud Organization.

L&#39;ID è una stringa alfanumerica di 24 caratteri seguita da `@AdobeOrg`. Se non conosci questo ID, contatta l&#39;Assistenza clienti.

### Escludi percorsi specifici

L&#39;Experience Cloud ID non viene caricato se l&#39;URL corrisponde a uno dei percorsi specificati.

(Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.

Fai clic su **[!UICONTROL Aggiungi]** per escludere un altro percorso.

### Consenso accordato

Utilizza le opzioni di consenso per determinare se richiedere ai visitatori il consenso ai servizi Adobe sul sito e se creare cookie per tracciare l&#39;attività dei visitatori.

Opt In il punto di riferimento centralizzato per tutte le librerie lato client della soluzione Platform per determinare se i cookie possono essere creati sul dispositivo o sul browser di un utente quando visita il sito. Opt In non fornisce supporto per raccogliere o memorizzare le preferenze di consenso dell&#39;utente.

**Abilitare Opt In?**

L&#39;opzione selezionata determina se il sito Web necessita del consenso per monitorare le attività di un visitatore sul sito Web.

Ci sono tre opzioni:

* **No:** non attende il consenso per il tracciamento del visitatore. Questo è il comportamento predefinito se non selezioni un&#39;opzione.
* **Sì:** attende il consenso per procedere al tracciamento del visitatore.
* **Determinato in fase di runtime utilizzando la funzione:** Determina in modo programmatico se il valore è true o false in fase di runtime. Se selezioni questa opzione, diventa disponibile il campo Select Data Element. Seleziona un elemento di dati che possa determinare se attendere il consenso. Questo elemento di dati viene risolto in un valore booleano. Ad esempio, puoi selezionare un elemento di dati che fornisca il consenso sulla base dell&#39;appartenenza o meno del Paese del visitatore all&#39;UE.

**Opt In Storage è abilitato?**

Se abilitata, il consenso viene memorizzato in un cookie di prime parti sul dominio. Se non è abilitata, le impostazioni di consenso vengono mantenute nel CMP o in un cookie che gestisci.

**Dominio cookie Opt In?**

Utilizza questa impostazione opzionale per specificare il dominio in cui viene memorizzato il cookie Opt In se l&#39;archiviazione è abilitata. Puoi immettere un dominio, oppure selezionare un elemento di dati contenente il dominio.

**Scadenza memorizzazione Opt In?**

Specifica quando scade il cookie Opt In se la memorizzazione è abilitata, in secondi.

Immetti un numero, quindi seleziona un&#39;unità di tempo dall&#39;elenco a discesa. Ad esempio, immetti 2 e seleziona **[!UICONTROL Settimane]**. Il valore predefinito è 13 mesi.

**Autorizzazioni?**

Trasmetti il consenso precedente alla libreria Opt In. Seleziona un elemento di dati contenente il consenso. Il tipo di elemento deve essere un oggetto o una stringa JSON. Sostituisce Pre Opt In Approvals.

Esempio:

`"{"aa":true,"aam":true,"ecid":true}"`

**Approvazioni antecedenti al consenso?**

Definisci quali categorie vengono approvate o rifiutate quando il visitatore non ha impostato alcuna preferenza. Si presume il consenso per le soluzioni selezionate dal momento in cui la pagina viene caricata. Il tipo di elemento deve essere un oggetto o una stringa JSON (esempio: `{aam: true}`).

### Variabili

Imposta coppie nome-valore come proprietà dell&#39;istanza Experience Cloud ID. Utilizza il menu a discesa per selezionare una variabile, quindi digita o seleziona un valore. Per informazioni su ciascuna variabile, consulta la [documentazione di Experience Cloud Identity Service](https://experiencecloud.adobe.com/resources/help/it_IT/mcvid/mcvid-overview.html).

## Tipi di azioni dell&#39;estensione Experience Cloud ID

In questa sezione sono descritti i tipi di azione disponibili nell&#39;estensione Experience Cloud ID.

### Tipi di azioni

#### Imposta ID cliente

Imposta uno o più ID cliente.

1. Immetti il codice di integrazione.

   Il codice di integrazione deve contenere il valore impostato come origine dati in Audience Manager o Customer Attributes.

1. Seleziona un valore.

   Il valore deve essere un ID utente. Gli elementi di dati più idonei per valori dinamici, come gli ID da un sistema interno specifico per il cliente.

1. Seleziona uno stato di autenticazione.

   Le opzioni disponibili sono:

   * Sconosciuto
   * autenticato
   * Utente disconnesso

1. (Facoltativo) Fai clic su **[!UICONTROL Aggiungi]** per impostare altri ID cliente.
1. Seleziona **[!UICONTROL Mantieni modifiche]**.
