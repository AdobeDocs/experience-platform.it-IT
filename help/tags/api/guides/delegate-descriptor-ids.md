---
title: ID descrittori dei delegati
description: Scopri gli ID descrittori dei delegati nell’API di Reactor e come collegano le risorse alle estensioni.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 100%

---

# ID descrittori dei delegati

Quando si utilizzano i tag in Adobe Experience Platform, tutte le funzionalità che è possibile implementare sul sito vengono fornite dalle estensioni. Le funzionalità fornite da ogni estensione sono definite dallo sviluppatore dell’estensione. Quando un’estensione viene implementata, viene fornita in bundle con le sue varie funzionalità sotto forma di un [pacchetto di estensione](../endpoints/extension-packages.md). Le funzionalità aggiunte dallo sviluppatore a un pacchetto di estensione sono considerate “delegati” di tale pacchetto.

A ogni delegato all’interno di un pacchetto di estensione viene assegnato un ID descrittore del delegato univoco. L’ID descrittore del delegato per una particolare risorsa comunica al sistema di che tipo di risorsa si tratta e a quale pacchetto di estensione appartiene.

## Sintassi

Un ID descrittore del delegato è costituito da tre stringhe unite dal carattere dei due punti (`::`) che rappresentano rispettivamente il nome del pacchetto di estensione, il tipo di delegato e il nome del delegato. Queste stringhe sono composte in modo da essere leggibili dall’utente, e vengono generate automaticamente e assegnate dal sistema quando viene acquisito un pacchetto di estensione.

Ad esempio, se un pacchetto di estensione denominato `example-package`ha un’azione denominata`custom-code`, tale azione avrà il seguente ID descrittore del delegato: `example-package::actions::custom-code`.

## Utilizzo degli ID descrittori dei delegati sulle risorse applicabili

È importante comprendere gli ID descrittori dei delegati ai fini della definizione dei componenti delle regole (eventi, condizioni e azioni) e degli elementi dati nelle API. Le sezioni seguenti illustrano come questi ID vengono utilizzati per ogni risorsa.

### Componenti della regola

Un [componente regola](../endpoints/rule-components.md) deve essere associato a un evento, una condizione o un’azione che appartiene a un pacchetto di estensione. Rappresenta il “tipo” del componente regola, in quanto si riferisce alla logica della regola generale (un evento, una condizione o un’azione). Durante la creazione di un componente regola, è quindi necessario fornire un ID descrittore del delegato per indicare a quale evento, condizione o azione deve essere associato il componente regola.

Ad esempio, per creare un componente regola evento basato su un evento `click` in un pacchetto di estensione `example-package`, il componente regola utilizza il seguente valore `delegate_descriptor_id`: `example-package::events::click`.

Per ulteriori informazioni, consulta la sezione sulla [creazione di un componente regola](../endpoints/rule-components.md#create).

### Elementi dati

Un [elemento dati](../endpoints/data-elements.md) deve essere associato a un pacchetto di estensione quando viene creato per la prima volta, in quanto ogni pacchetto di estensione definisce i tipi compatibili per i propri elementi dati delegati e il comportamento previsto.

Ad esempio, per creare un elemento dati che utilizza il tipo `cookie` definito dal pacchetto di estensione `example-package`, l’elemento dati utilizza il seguente valore `delegate_descriptor_id`: `example-package::dataElements::cookie`.

Per ulteriori informazioni, consulta la sezione sulla [creazione di un elemento dati](../endpoints/data-elements.md#create).

### Estensioni

Quando viene creata, un’[estensione](../endpoints/extensions.md) viene associata automaticamente a un pacchetto di estensione ed è rappresentata all’interno dell’oggetto `relationships` dell’estensione. Se l’estensione richiede impostazioni personalizzate, richiede anche un ID descrittore del delegato.

>[!NOTE]
>
>Per le estensioni che non richiedono impostazioni personalizzate, l’ID descrittore del delegato non è necessario.

Ad esempio, per aggiungere un ID descrittore delegato a un’estensione che appartiene al pacchetto di estensione `example-package`, l’estensione utilizza il seguente valore `delegate_descriptor_id`: `example-package::extensionConfiguration::config`.

Per ulteriori informazioni, consulta la guida sulla [creazione di un’estensione](../endpoints/extensions.md#create).
