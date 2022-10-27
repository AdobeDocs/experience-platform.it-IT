---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;enum;campo;
solution: Experience Platform
title: Definire i campi enumerati e i valori consigliati nell’interfaccia utente
description: Scopri come definire enum e valori consigliati per i campi stringa nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 89ada47cb6e0b204d8f2f19e7e9b6f31bf347964
workflow-type: tm+mt
source-wordcount: '1257'
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

![Immagine che mostra l’opzione Enum &amp; Suggested Values abilitata per un campo stringa nell’interfaccia utente](../../images/ui/fields/enum/enum-options-selected.png)

Questo documento illustra come definire enum e valori suggeriti nel [!UICONTROL Schemi] Area di lavoro dell’interfaccia utente. Per una rapida panoramica degli enum e dei valori suggeriti, tra cui come configurarli nell’interfaccia utente e i relativi effetti a valle, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Definire un enum {#enum}

Seleziona **[!UICONTROL Enum e valori consigliati]**, quindi seleziona **[!UICONTROL Enum]**. Vengono visualizzati altri controlli che consentono di specificare i vincoli di valore per l’enum. Per aggiungere un vincolo, seleziona **[!UICONTROL Aggiungi riga]**.

![Immagine che mostra l’opzione Enums selezionata nell’interfaccia utente](../../images/ui/fields/enum/enum-add-row.png)

Sotto la **[!UICONTROL Valore]** È necessario specificare il valore esatto a cui si desidera vincolare il campo. Facoltativamente, puoi fornire un **[!UICONTROL Nome visualizzato]** anche per il vincolo, che influisce sul modo in cui il valore verrà rappresentato nella segmentazione.

Continua a utilizzare **[!UICONTROL Aggiungi riga]** per aggiungere i vincoli desiderati e le etichette facoltative all’enum, oppure seleziona l’icona Elimina (![Immagine dell’icona Elimina](../../images/ui/fields/enum/remove-icon.png)) accanto a una riga aggiunta in precedenza per rimuoverla. Al termine, seleziona **[!UICONTROL Applica]** per applicare le modifiche allo schema.

![Immagine che mostra i valori enum e i nomi visualizzati compilati per il campo stringa nell’interfaccia utente](../../images/ui/fields/enum/enum-confirm.png)

L’area di lavoro viene aggiornata per riflettere le modifiche. Quando esplori questo schema in futuro, puoi visualizzare e modificare i vincoli per il campo enum nella barra a destra.

## Definire i valori suggeriti {#suggested-values}

Seleziona **[!UICONTROL Enum e valori consigliati]**, quindi seleziona **[!UICONTROL Valori consigliati]** per visualizzare controlli aggiuntivi. Da qui, seleziona **[!UICONTROL Aggiungi riga]** per iniziare ad aggiungere valori consigliati.

![Immagine che mostra l’opzione Valori suggeriti selezionata nell’interfaccia utente](../../images/ui/fields/enum/suggested-add-row.png)

Sotto la **[!UICONTROL Nome visualizzato]** fornisci un nome descrittivo per il valore come desideri che appaia nell’interfaccia utente Segmentazione. Per aggiungere altri valori consigliati, seleziona **[!UICONTROL Aggiungi riga]** e ripetere il processo in base alle esigenze. Per rimuovere una riga aggiunta in precedenza, seleziona ![l’icona Elimina](../../images/ui/fields/enum/remove-icon.png) accanto alla riga in questione.

Al termine, seleziona **[!UICONTROL Applica]** per applicare le modifiche allo schema.

![Immagine che mostra i valori enum e i nomi visualizzati compilati per il campo stringa nell’interfaccia utente](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Si verifica un ritardo di circa cinque minuti perché i valori consigliati aggiornati di un campo si riflettano nell’interfaccia utente Segmentazione.

### Gestione dei valori consigliati per i campi standard

Alcuni campi dei componenti XDM standard contengono i valori consigliati, ad esempio `eventType` dal [[!UICONTROL ExperienceEvent XDM] Classe](../../classes/experienceevent.md). Mentre è possibile creare valori aggiuntivi consigliati per un campo standard, non è possibile modificare o rimuovere i valori suggeriti non definiti dall’organizzazione. Quando visualizzi un campo standard nell’interfaccia utente, i valori suggeriti vengono visualizzati ma sono di sola lettura.

![Immagine che mostra i valori enum e i nomi visualizzati compilati per il campo stringa nell’interfaccia utente](../../images/ui/fields/enum/suggested-standard.png)

Per aggiungere nuovi valori consigliati per un campo standard, selezionare **[!UICONTROL Aggiungi riga]**. Per rimuovere un valore suggerito precedentemente aggiunto dall’organizzazione, seleziona ![l’icona Elimina](../../images/ui/fields/enum/remove-icon.png) accanto alla riga in questione.

![Immagine che mostra i valori enum e i nomi visualizzati compilati per il campo stringa nell’interfaccia utente](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Regole di evoluzione per gli enum e i valori consigliati {#evolution}

Dopo aver utilizzato uno schema con un campo enum per acquisire dati in Platform, qualsiasi ulteriore modifica apportata alla definizione dello schema deve essere conforme ai dati già presenti nel sistema. In generale, le modifiche apportate a un campo esistente possono solo rendere tale campo **less** restrittivo. Un campo non può essere reso più restrittivo di quanto non sia già.

Quando si tratta di enum e valori suggeriti, le seguenti regole si applicano dopo l’acquisizione:

* You **PUÒ** aggiungi valori consigliati per i campi standard e personalizzati con valori consigliati esistenti.
* You **PUÒ** rimuovi i valori consigliati dai campi personalizzati con valori consigliati esistenti.
* You **PUÒ** aggiungi nuovi valori enum per un campo enum personalizzato esistente.
* You **PUÒ** cambia i valori enum di un campo personalizzato solo in valori consigliati o li converte in una stringa senza enum o valori consigliati. **Questa opzione non può essere annullata dopo l&#39;applicazione.**
* You **IMPOSSIBILE** rimuovi enum o valori consigliati dai campi standard.
* You **IMPOSSIBILE** aggiungi valori enum a un campo senza enum esistente.
* You **IMPOSSIBILE** rimuovi meno di tutti i valori enum esistenti per un campo personalizzato.
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

Per scoprire come definire altri tipi di campi XDM nel [!DNL Schema Editor], consulta la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special).
