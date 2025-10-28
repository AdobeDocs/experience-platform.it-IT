---
title: Riferimento per la creazione di regole dei criteri di consenso
description: Scopri come utilizzare i tipi di dati XDM, gli operatori supportati e la logica avanzata per creare regole granulari dei criteri di consenso nell’interfaccia utente di Adobe Experience Platform.
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Riferimento per la creazione di regole dei criteri di consenso

Utilizzare questo riferimento alla logica avanzata delle regole per impostare regole precise e giuridicamente valide nella clausola **[!UICONTROL Then]** del generatore di criteri di consenso in Adobe Experience Platform.

![L&#39;interfaccia del generatore dei criteri di consenso evidenzia la sezione della clausola [!UICONTROL Then], in cui gli utenti definiscono le condizioni della regola.](../images/policies/multiple-rules.png)

Scopri come le regole dei criteri si applicano alla struttura e ai tipi di dati sul consenso per applicare in modo preciso le preferenze di consenso dei clienti.

Leggi questo documento per scoprire come filtrare i profili in base al consenso navigando nei campi contenitore nello schema XDM e selezionando un campo primitivo. Quindi utilizza l’operatore appropriato per definire il valore esatto che un profilo deve corrispondere.

## Prerequisiti

Prima di utilizzare questo riferimento, assicurati che la configurazione dei criteri di consenso sia completa e che tu comprenda i concetti fondamentali dell’architettura dei dati e del framework di governance di Adobe Experience Platform.

Assicurati di soddisfare i seguenti prerequisiti:

* **Impostazione dei criteri completata**: hai creato o iniziato a creare un criterio di consenso nell&#39;interfaccia utente di Adobe Experience Platform. Per i passaggi dettagliati, consulta la [guida utente dei criteri di utilizzo dei dati](user-guide.md#consent-policy).

* **Familiarità con le strutture di dati**: questo riferimento richiede una conoscenza operativa dei seguenti concetti di base:
   * **XDM e schema di unione**: scopri come le strutture del modello dati di esperienza definiscono le relazioni tra i dati e come lo schema di unione rappresenta i profili cliente unificati. Per ulteriori informazioni, consulta la [Panoramica del sistema XDM](../../xdm/home.md).
   * **Framework di governance dei dati**: scopri in che modo Adobe Experience Platform applica i criteri di utilizzo dei dati e le regole di governance. Per informazioni dettagliate, consulta la [Panoramica sulla governance dei dati](../home.md).
   * **Elaborazione del consenso del cliente**: scopri come i dati sul consenso vengono raccolti, memorizzati e applicati all&#39;interno dei flussi di lavoro dell&#39;esperienza del cliente. Consulta la [panoramica sull&#39;elaborazione del consenso](../../landing/governance-privacy-security/consent/adobe/overview.md).

## Concetti di base: campi primitivi e contenitori

Leggi questa sezione per scoprire come le regole dei criteri di consenso utilizzano diversi tipi di campo negli schemi XDM. La distinzione tra campi contenitore e campi primitivi consente di selezionare il campo e l’operatore corretti durante la definizione delle condizioni dei criteri.

### Tipi di campo supportati e logica della regola

I criteri di consenso supportano più tipi di campo, ciascuno con operatori specifici per la creazione di condizioni delle regole. I tipi di campo sono raggruppati in due categorie: **tipi contenitore** e **tipi primitivi**.

### Tipi di contenitori (navigazione schema)

I tipi di contenitore organizzano i dati del consenso, ma non possono essere utilizzati direttamente nelle condizioni dei criteri. Fungono da percorsi di navigazione per raggiungere i campi primitivi che contengono i valori effettivi.

| Tipo di contenitore | Descrizione |
|----------------|-------------|
| **Oggetto** | Contenitore con uno schema fisso che contiene più campi di tipi diversi. |
| **Array** | Contenitore contenente più valori dello stesso tipo. |
| **Mappa** | Contenitore con chiavi dinamiche che può contenere oggetti o altri tipi di campi. |

>[!IMPORTANT]
>
>I campi contenitore non possono essere selezionati direttamente nelle condizioni dei criteri di consenso. È necessario passare ai contenitori per selezionare **campi primitivi** (ad esempio stringa, numero o booleano) per la creazione di regole. Gli operatori contenitore vengono utilizzati solo per la navigazione dello schema e non per l’impostazione di condizioni dei criteri.

### Tipi primitivi (condizioni regola)

I campi primitivi contengono i valori dei dati di consenso effettivi (ad esempio, `true` o `"weekly"`) e sono gli unici tipi di campo che possono essere utilizzati per definire le condizioni dei criteri.

La tabella seguente descrive ogni tipo primitivo supportato e gli operatori disponibili.

| Tipo primitivo | Operatori supportati | Descrizione |
|----------------|---------------------|-------------|
| **Stringa** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Attributi di consenso basati su testo. |
| **Numero** | `is equal to`, `is not equal to`, `is greater than`, `is less than`, `exists`, `does not exist` | Attributi di consenso numerici. |
| **Booleano** | `is equal to`, `is not equal to` | Valori di consenso true o false. |
| **Data** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Attributi di consenso basati sulla data. |


## Utilizzo di strutture di dati complesse

Leggi questa sezione per scoprire come navigare tra i contenitori nidificati nello schema di consenso per raggiungere i campi primitivi. Introduce pattern di schema comuni e spiega come le strutture più profonde consentano una logica di consenso più granulare.

### Gestione di strutture di schema nidificate e complesse

Gli schemi di consenso complessi spesso includono strutture di contenitori nidificati che supportano la gestione flessibile e scalabile dei dati. Poiché le regole dei criteri possono fare riferimento solo a campi primitivi, è necessario spostarsi tra le gerarchie dei contenitori per raggiungere i campi che possono essere utilizzati nelle condizioni dei criteri di consenso. Una nidificazione più approfondita consente un targeting delle regole più granulare e specifico.

I pattern comuni dei contenitori nidificati includono:

* **Mappa della mappa** - Chiavi dinamiche che contengono altre mappe.
* **Mappa dell&#39;oggetto** - Chiavi dinamiche che contengono oggetti con schemi fissi.
* **Array di mappa** - Array che contengono mappe con chiavi dinamiche.
* **Array dell&#39;oggetto** - Array che contengono oggetti con schemi fissi.
* **Oggetto con proprietà mappa o matrice** - Oggetti che includono campi mappa o matrice.

### Esempio di struttura del campo

La struttura seguente funge da riferimento visivo per gli esempi di regole in questa guida.

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## Creazione di regole avanzate per tipo di campo

Leggi questa sezione per una guida dettagliata sulla creazione di regole dei criteri di consenso basate sul tipo di campo. Scoprirai come configurare la logica delle regole per booleani, mappe, oggetti e array per acquisire condizioni di consenso precise.

### Componenti e passaggi per la creazione di regole

Per creare regole di criteri di consenso efficaci è necessario comprendere come navigare nella struttura dello schema e applicare gli operatori corretti per ogni tipo di campo. Ogni regola segue lo stesso approccio di base: passa a un campo primitivo, seleziona l’operatore appropriato e definisci la condizione che deve essere soddisfatta.

Per creare una regola, segui la procedura riportata di seguito:

1. **Selezionare un campo** - Passare tra i campi contenitore per raggiungere un campo primitivo.
2. **Scegli un operatore** - Seleziona l&#39;operatore supportato dal tipo di campo.
   ![Pannello di navigazione dello schema gerarchico, che mostra un utente che espande un contenitore per raggiungere un campo primitivo.](../images/policies/consent-policy-map-field.png)
3. **Imposta un valore**. Definisci il valore o la condizione da associare.
4. **Corrispondenza chiavi mappa** - Scegliere se impostare come destinazione una chiave specifica o una corrispondenza tra tutte le chiavi di una mappa.
5. **Aggiungi condizioni** - Combina più regole utilizzando AND o OR, a seconda delle necessità.

### Utilizzo di campi booleani (logica di consenso implicito)

I campi booleani memorizzano i valori di consenso true o false e rappresentano gli attributi di consenso più comuni. L&#39;operatore `is not equal to` consente di includere profili che non hanno esplicitamente rinunciato, supportando scenari di consenso implicito.

**Operatori e risultati booleani**

| Operatore | Valore | Risultato |
|----------|-------|--------|
| `is equal to` | `true` | Include i profili con consenso esplicito (`true`). |
| `is equal to` | `false` | Include i profili con rinuncia esplicita (`false`). |
| `is not equal to` | `true` | Include i profili senza consenso esplicito (`false` o mancanti). |
| `is not equal to` | `false` | Include i profili che non hanno esplicitamente rinunciato (`true` o mancanti). |

**Esempio: consenso e-mail implicito**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### Utilizzo dei campi mappa (preferenze dinamiche)

I campi mappa memorizzano coppie chiave-valore con chiavi dinamiche, a differenza di oggetti che hanno schemi fissi. Le mappe vengono spesso utilizzate nei centri delle preferenze, dove è possibile aggiungere nuove categorie senza dover aggiornare lo schema. Puoi eseguire il targeting di chiavi specifiche o utilizzare la corrispondenza dei caratteri jolly in tutte le chiavi.

**Corrispondenza chiave specifica**

Utilizzare questo approccio per eseguire il targeting di una categoria di preferenze specifica.

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**Qualsiasi chiave corrispondente**

Utilizzare l&#39;opzione della casella di controllo &quot;**[!UICONTROL find any matching item]**&quot; per trovare una corrispondenza tra tutte le chiavi dinamiche in una mappa.

![Generatore regole dei criteri che visualizza la casella di controllo &quot;Trova qualsiasi elemento corrispondente&quot; per i campi Mappa, utilizzati per associare i valori in tutte le chiavi dinamiche.](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### Utilizzo dei campi oggetto (navigazione fissa)

I campi oggetto fungono da contenitori con schemi fissi. Vengono utilizzati solo per la navigazione e non è possibile farvi riferimento direttamente nelle condizioni dei criteri.

**Esempio di navigazione**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**Caso d&#39;uso di esempio:**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### Utilizzo dei campi array (più valori)

I campi array contengono più valori dello stesso tipo e richiedono una gestione diversa a seconda che memorizzino primitive o oggetti. Le opzioni di navigazione e operatore variano in base al tipo di array.

**Esempio di array di primitive**

Utilizzare l&#39;operatore `contains` per identificare i profili in base a valori specifici all&#39;interno di un array.

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**Esempio di array di oggetti**

Accedi all’array per accedere ai campi primitivi all’interno degli oggetti nidificati.

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## Combinazione di regole con logica complessa

Questa sezione spiega come combinare più condizioni di regola utilizzando l’operatore logico AND o OR. Scoprirai come gli operatori logici lavorano insieme per definire criteri di consenso avanzati e a più condizioni.

### Combinazione di più condizioni (AND o OR)

Puoi combinare più condizioni di regola utilizzando l’operatore logico AND o OR per creare criteri di consenso più sofisticati destinati a segmenti di profilo specifici.\
**AND logic** richiede che tutte le condizioni siano vere, generando corrispondenze di pubblico più strette.\
**OR logic** consente a qualsiasi condizione di essere true, espandendo la portata del pubblico.

Nell’interfaccia dei criteri di consenso, utilizza il selettore logico visualizzato tra le condizioni della regola per passare dalla logica AND a quella OR.

### Esempio generale di regola complessa

L’esempio seguente combina lo stato del consenso di base con la frequenza delle preferenze per creare un segmento di destinazione.

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### Logica avanzata per array di oggetti

Quando si combinano condizioni all&#39;interno di array di oggetti, il comportamento dipende dall&#39;utilizzo della logica AND o OR tra le condizioni.

**Esempio: array di oggetti con condizioni AND**

Usa la logica AND quando tutte le condizioni devono essere applicate all&#39;elemento di array *same*.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>**Best practice per la logica AND**
>
>Quando si creano condizioni di array basate su AND, tenere presenti i seguenti comportamenti chiave:
>
>* Utilizzare la logica AND quando tutte le condizioni devono essere applicate allo **stesso elemento di matrice**.
>* Ricorda che AND crea un targeting restrittivo (un numero inferiore di profili corrisponderà).
>* Non si prevede che la logica AND corrisponda tra più voci di array; si applica all’interno di ogni voce.
>* Evita l’utilizzo della logica AND quando hai bisogno di una corrispondenza flessibile tra le voci.

>[!IMPORTANT]
>
>Con la logica AND, ogni voce di array deve soddisfare tutte le condizioni specificate contemporaneamente. Questo comportamento è ideale quando devi far corrispondere attributi combinati, ad esempio categorie abilitate e promozionali.

>[!NOTE]
>
>La logica AND si applica alla stessa voce di array **solo per gli array di oggetti.**\
>Per gli array di primitive, la logica AND viene valutata a livello di campo in tutto l’array.

**Esempio: array di oggetti con condizioni OR**

Utilizza la logica OR per creare corrispondenze di pubblico inclusive consentendo a qualsiasi condizione di essere vera tra le voci dell’array.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### Passaggi successivi

Dopo aver generato e perfezionato le regole dei criteri di consenso, utilizza le risorse seguenti per finalizzare la configurazione, convalidare l’applicazione dei criteri e rivedere i modelli di dati sottostanti.

* **Flusso di lavoro per la creazione di criteri**: implementa le regole definite nell&#39;interfaccia utente del generatore di criteri con la [Guida all&#39;interfaccia utente dei criteri di consenso](user-guide.md#consent-policy.md)
* **Valutazione e applicazione dei criteri di consenso**: verifica in che modo i criteri abilitati influiscono sull&#39;attivazione del pubblico e sull&#39;utilizzo dei dati del profilo. Per ulteriori informazioni, vedere la [Guida all&#39;applicazione automatica dei criteri](../enforcement/auto-enforcement.md)
* **Tipi di dati di consenso XDM**: fai riferimento alle strutture di schema e alle definizioni di campo specifiche per gli attributi di consenso utilizzati nelle regole dei criteri. Consulta la guida del tipo di dati [Consensi e preferenze XDM](../../xdm/data-types/consents.md).
