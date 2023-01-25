---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;enum;campo;
solution: Experience Platform
title: Definire i campi enumerati e i valori consigliati nell’interfaccia utente
description: Scopri come definire enum e valori consigliati per i campi stringa nell’interfaccia utente di Experience Platform.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f770ba8668c5154b2cf5a57ba61d771ca34ab2d8
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Definire enum e valori consigliati nell’interfaccia utente {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Enum e valori consigliati"
>abstract="Un **Enum** vincola un campo stringa affinché consenta l’acquisizione solo dei dati che corrispondono a un set predefinito di valori. A ogni vincolo enum può essere assegnato un **Nome visualizzato** popola i menu a discesa degli attributi nell’interfaccia utente Segmentazione. **Valori consigliati** per un campo non limitare l’acquisizione e determinare solo i nomi visualizzati visualizzati in Segmentazione. Se si dispone di più schemi che condividono un campo appartenente a una classe o a un gruppo di campi comune e si definiscono enum o valori consigliati diversi per quel campo tra ogni schema, tali valori vengono uniti e aggiunti nello schema di unione."

In Experience Data Model (XDM), è possibile assegnare a un campo stringa un set predefinito di valori accettati o consigliati per controllare meglio quali valori vengono acquisiti in quel campo o come si comporterà nella segmentazione.

**[!UICONTROL Enum]** vincolare i valori che possono essere acquisiti per un campo stringa a un set predefinito. Se tenti di acquisire dati in un campo enum e il valore non corrisponde a nessuno di quelli definiti nella relativa configurazione, l’acquisizione verrà negata.

A differenza degli enum, il **[!UICONTROL Valori consigliati]** consente di indicare un set di valori consigliati per un campo stringa che non vincola i valori che è possibile acquisire. Al contrario, i valori suggeriti influenzano i valori predefiniti disponibili nel [Interfaccia utente di segmentazione](../../../segmentation/ui/overview.md) quando si include il campo stringa come attributo.

Quando [definizione di un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform e l’impostazione del tipo su [!UICONTROL Stringa], ti viene offerta l’opzione di definire un [enum](#enum) o [valori consigliati](#suggested-values) per quel campo.

![L’opzione Enum &amp; Suggested Values è abilitata per un campo stringa nell’interfaccia utente.](../../images/ui/fields/enum/enum-options-selected.png)

Questo documento illustra come definire enum e valori suggeriti nel [!UICONTROL Schemi] Area di lavoro dell’interfaccia utente. Per una rapida panoramica degli enum e dei valori suggeriti, tra cui come configurarli nell’interfaccia utente e i relativi effetti a valle, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Definire un enum {#enum}

Seleziona **[!UICONTROL Enum e valori consigliati]**, quindi seleziona **[!UICONTROL Enum]**. Vengono visualizzati altri controlli che consentono di specificare i vincoli di valore per l’enum. Per aggiungere un vincolo, seleziona **[!UICONTROL Aggiungi riga]**.

![Opzione enumerazioni selezionata nell’interfaccia utente.](../../images/ui/fields/enum/enum-add-row.png)

Sotto la **[!UICONTROL Valore]** È necessario specificare il valore esatto a cui si desidera vincolare il campo. Facoltativamente, puoi fornire un **[!UICONTROL Nome visualizzato]** anche per il vincolo, che influisce sul modo in cui il valore verrà rappresentato nella segmentazione.

Continua a utilizzare **[!UICONTROL Aggiungi riga]** per aggiungere i vincoli desiderati e le etichette facoltative all’enum, oppure seleziona l’icona Elimina (![Immagine dell’icona Elimina](../../images/ui/fields/enum/remove-icon.png)) accanto a una riga aggiunta in precedenza per rimuoverla. Al termine, seleziona **[!UICONTROL Applica]** per applicare le modifiche allo schema.

![Valori enum e nomi visualizzati compilati per il campo stringa nell&#39;interfaccia utente.](../../images/ui/fields/enum/enum-confirm.png)

L’area di lavoro viene aggiornata per riflettere le modifiche. Quando esplori questo schema in futuro, puoi visualizzare e modificare i vincoli per il campo enum nella barra a destra.

## Definire i valori suggeriti {#suggested-values}

Seleziona **[!UICONTROL Enum e valori consigliati]**, quindi seleziona **[!UICONTROL Valori consigliati]** per visualizzare controlli aggiuntivi. Da qui, seleziona **[!UICONTROL Aggiungi riga]** per iniziare ad aggiungere valori consigliati.

![L’opzione Valori consigliati selezionata nell’interfaccia utente.](../../images/ui/fields/enum/suggested-add-row.png)

Sotto la **[!UICONTROL Nome visualizzato]** fornisci un nome descrittivo per il valore come desideri che appaia nell’interfaccia utente Segmentazione. Per aggiungere altri valori consigliati, seleziona **[!UICONTROL Aggiungi riga]** e ripetere il processo in base alle esigenze. Per rimuovere una riga aggiunta in precedenza, seleziona ![l’icona Elimina](../../images/ui/fields/enum/remove-icon.png) accanto alla riga in questione.

Al termine, seleziona **[!UICONTROL Applica]** per applicare le modifiche allo schema.

![Valori enum e nomi visualizzati compilati per il campo stringa nell&#39;interfaccia utente.](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Si verifica un ritardo di circa cinque minuti perché i valori consigliati aggiornati di un campo si riflettano nell’interfaccia utente Segmentazione.

### Gestione dei valori consigliati per i campi standard {#standard-fields}

Alcuni campi dei componenti XDM standard contengono i valori consigliati, ad esempio `eventType` dal [[!UICONTROL ExperienceEvent XDM] Classe](../../classes/experienceevent.md) è inoltre possibile creare valori consigliati aggiuntivi per questi campi standard nello stesso modo in cui si utilizzerebbero per i campi personalizzati. Puoi anche disabilitare uno qualsiasi dei valori consigliati standard non adatti ai tuoi casi d’uso, ma non possono essere rimossi direttamente dalla definizione del campo.

>[!IMPORTANT]
>
>È possibile disattivare solo i valori consigliati per i campi standard che non hanno un vincolo enum corrispondente. In altre parole, se **[!UICONTROL Enum]** è abilitata al posto di **[!UICONTROL Valori consigliati]**, il campo è vincolato come un enum e tali vincoli non possono essere disattivati.
>
>Consulta la sezione [sezione sottostante](#evolution) per ulteriori informazioni sulle regole per l&#39;aggiornamento degli enum e sui valori consigliati per i campi dello schema esistenti.

Per disattivare un valore consigliato standard, seleziona l’opzione accanto al valore in questione. È possibile disattivare qualsiasi combinazione di valori suggeriti, inclusi tutti.

![Alcuni dei valori standard suggeriti per [!UICONTROL Tipo evento] campo disabilitato nell’interfaccia utente.](../../images/ui/fields/enum/suggested-standard.png)

Per aggiungere nuovi valori consigliati per un campo standard, selezionare **[!UICONTROL Aggiungi riga]**. Per rimuovere un valore suggerito precedentemente aggiunto dall’organizzazione, seleziona ![l’icona Elimina](../../images/ui/fields/enum/remove-icon.png) accanto alla riga in questione.

![Valori consigliati personalizzati aggiunti a un campo stringa standard nell’interfaccia utente.](../../images/ui/fields/enum/suggested-standard-add.png)

## Regole di evoluzione per gli enum e i valori consigliati {#evolution}

Dopo aver utilizzato uno schema con un campo enum per acquisire dati in Platform, qualsiasi ulteriore modifica apportata alla definizione dello schema deve essere conforme ai dati già presenti nel sistema. In generale, le modifiche apportate a un campo esistente possono solo rendere tale campo **less** restrittivo. Un campo non può essere reso più restrittivo di quanto non sia già.

Quando si tratta di enum e valori suggeriti, le seguenti regole si applicano dopo l’acquisizione:

* You **PUÒ** aggiungi valori consigliati a qualsiasi campo con valori suggeriti esistenti.
* You **PUÒ** rimuovi i valori consigliati personalizzati dai campi con valori suggeriti esistenti.
* You **PUÒ** disabilita i valori consigliati standard dai campi con solo valori consigliati e senza vincoli di enumerazione.
* You **PUÒ** aggiungi nuovi valori enum per un campo enum personalizzato esistente.
* You **PUÒ** cambia i valori enum di un campo personalizzato solo in valori consigliati o li converte in una stringa senza enum o valori consigliati. **Questa opzione non può essere annullata dopo l&#39;applicazione.**
* You **IMPOSSIBILE** aggiungi o rimuovi vincoli enum dai campi standard.
* You **IMPOSSIBILE** rimuovi i valori consigliati dai campi standard (disattiva solo).
* You **IMPOSSIBILE** aggiungi vincoli enum ai campi senza enum esistente.
* You **IMPOSSIBILE** rimuovi meno di tutti i vincoli enum esistenti per un campo personalizzato.
* You **IMPOSSIBILE** passa da valori consigliati a un enum.

## Unione di regole per enum e valori consigliati {#merging}

Se più schemi utilizzano lo stesso campo enum con diverse configurazioni e tali schemi sono inclusi in un’unione, alcune regole si applicano quando si tratta di riconciliare le differenze enum. Le regole esatte dipendono dal fatto che gli schemi facciano riferimento allo stesso campo standard (come `eventType`) o se fanno riferimento allo stesso percorso di campo personalizzato in gruppi di campi diversi.

Se si fa riferimento allo stesso campo standard:

* Eventuali valori suggeriti aggiuntivi sono **AGGIUNTO** nell&#39;unione.
* Gli aggiornamenti apportati ai valori suggeriti per la stessa chiave enum sono **AGGIORNATO** nell&#39;unione.

Se si fa riferimento allo stesso percorso di campo personalizzato in diversi gruppi di campi:

* Eventuali valori suggeriti aggiuntivi sono **AGGIUNTO** nell&#39;unione.
* Se lo stesso valore suggerito aggiuntivo è definito in più schemi, questi valori sono **UNITO** nell&#39;unione. In altre parole, lo stesso valore suggerito non verrà visualizzato due volte dopo l’unione.

## Limiti di convalida

A causa delle attuali limitazioni del sistema, ci sono due casi in cui un enum non viene convalidato dal sistema durante l&#39;acquisizione:

1. L&#39;enum è definito su un [campo matrice](./array.md).
1. L&#39;enum è definito a più livelli nella gerarchia dello schema.

## Passaggi successivi

Questa guida illustra come definire enum e valori consigliati per i campi stringa nell’interfaccia utente di . Per informazioni su come gestire gli enum e i valori consigliati utilizzando l’API del Registro di sistema dello schema, consulta quanto segue [tutorial](../../tutorials/suggested-values.md).

Per scoprire come definire altri tipi di campi XDM nel [!DNL Schema Editor], consulta la panoramica su [definizione dei campi nell’interfaccia utente.](./overview.md#special).
