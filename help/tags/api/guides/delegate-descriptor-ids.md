---
title: ID descrittori delegati
description: Scopri gli ID del descrittore delegato nell’API di Reactor e come collegano le risorse con le estensioni.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# ID dei descrittori delegati

Quando si utilizzano i tag in Adobe Experience Platform, tutte le funzionalità che è possibile distribuire sul sito vengono fornite dalle estensioni. Le funzionalità fornite da ogni estensione sono definite dallo sviluppatore di estensioni. Quando un&#39;estensione viene distribuita, viene fornita in bundle con le sue varie funzionalità sotto forma di un [pacchetto di estensione](../endpoints/extension-packages.md). Le funzionalità aggiunte dagli sviluppatori a un pacchetto di estensione sono considerate &quot;delegati&quot; di tale pacchetto.

A ogni delegato all&#39;interno di un pacchetto di estensione viene assegnato un ID descrittore delegato univoco. L&#39;ID del descrittore delegato per una particolare risorsa comunica al sistema di che tipo di risorsa è e a quale pacchetto di estensione appartiene.

## Sintassi

Un ID descrittore delegato è costituito da tre stringhe unite da caratteri a due punti (`::`) che rappresentano rispettivamente il nome del pacchetto di estensione, il tipo di delegato e il nome del delegato. Queste stringhe sono composte in modo da essere leggibili dall&#39;utente e vengono generate automaticamente e assegnate dal sistema quando viene acquisito un pacchetto di estensione.

Ad esempio, se un pacchetto di estensione denominato `example-package` ha un&#39;azione denominata `custom-code`, tale azione avrà il seguente ID descrittore delegato: `example-package::actions::custom-code`.

## Utilizzo degli ID del descrittore delegato sulle risorse applicabili

Gli ID dei descrittori delegati sono importanti per comprendere quando si tratta di definire i componenti della regola (eventi, condizioni e azioni) e gli elementi dati nell’API. Le sezioni seguenti illustrano come questi ID vengono utilizzati per ogni risorsa.

### Componenti della regola

Un [componente regola](../endpoints/rule-components.md) deve essere associato a un evento, una condizione o un&#39;azione che appartiene a un pacchetto di estensione. Rappresenta il &quot;tipo&quot; del componente regola in quanto si riferisce alla logica della regola generale (un evento, una condizione o un&#39;azione). Pertanto, durante la creazione di un componente regola, è necessario fornire un ID descrittore delegato per indicare a quale evento, condizione o azione deve essere associato il componente regola.

Ad esempio, per creare un componente regola evento basato su un evento `click` in un pacchetto di estensione `example-package`, il componente regola utilizza il seguente valore `delegate_descriptor_id`: `example-package::events::click`.

Per ulteriori informazioni, consulta la sezione su [creazione di un componente regola](../endpoints/rule-components.md#create) .

### Elementi dati

Un [elemento dati](../endpoints/data-elements.md) deve essere associato a un pacchetto di estensione quando viene creato per la prima volta, in quanto ogni pacchetto di estensione definisce i tipi compatibili per i propri elementi dati delegati e il comportamento previsto.

Ad esempio, per creare un elemento dati che utilizza il tipo `cookie` come definito dal pacchetto di estensione `example-package`, l&#39;elemento dati utilizza il seguente valore `delegate_descriptor_id`: `example-package::dataElements::cookie`.

Per ulteriori informazioni, consulta la sezione su [creazione di un elemento dati](../endpoints/data-elements.md#create) .

### Estensioni

Un&#39;estensione [](../endpoints/extensions.md) viene associata automaticamente a un pacchetto di estensione al momento della prima creazione ed è rappresentata all&#39;interno dell&#39;oggetto `relationships` dell&#39;estensione. Se l&#39;estensione richiede impostazioni personalizzate, richiede anche un ID descrittore delegato.

>[!NOTE]
>
>Per le estensioni che non richiedono impostazioni personalizzate non è necessario un ID descrittore delegato.

Ad esempio, per aggiungere un ID descrittore delegato a un&#39;estensione che appartiene al pacchetto di estensione `example-package`, l&#39;estensione utilizza il seguente valore `delegate_descriptor_id`: `example-package::extensionConfiguration::config`.

Per ulteriori informazioni, consulta la guida sulla [creazione di un&#39;estensione](../endpoints/extensions.md#create) .