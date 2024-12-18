---
title: Tipo di dati dettagli servizio virtuale
description: Scopri il tipo di dati Virtual Service Detail Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: bde7363c-43b7-402d-96b2-7aa0160cd2ea
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# [!UICONTROL Dettagli servizio virtuale] tipo di dati

[!UICONTROL Virtual Service Detail] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli di contatto del servizio virtuale. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati Dettagli servizio virtuale](../../../images/healthcare/data-types/virtual-service-detail.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Punto di contatto indirizzo] | `addressContactPoint` | [[!UICONTROL Punto di contatto]](../data-types/contact-point.md) | I dettagli di un punto di contatto mediato dalla tecnologia, ad esempio telefono, fax o e-mail. |
| [!UICONTROL Dettagli contatto esteso indirizzo] | `addressExtendedContactDetail` | [[!UICONTROL Dettagli contatti estesi]](../data-types/extended-contact-detail.md) | Informazioni di contatto estese. |
| [!UICONTROL Tipo di canale] | `channelType` | [[!UICONTROL Codifica]](../data-types/coding.md) | Tipo di servizio virtuale a cui connettersi, ad esempio Team, Zoom o WhatsApp. |
| [!UICONTROL Informazioni aggiuntive] | `additionalInfo` | Array di stringhe | L’indirizzo per visualizzare i dettagli di connessione alternativi, rappresentati come URI. |
| [!UICONTROL Stringa indirizzo] | `addressString` | Stringa | Indirizzo da utilizzare per la connessione al servizio virtuale. |
| [!UICONTROL Url Indirizzo] | `addressUrl` | Stringa | URL da utilizzare per la connessione al servizio virtuale, rappresentato come URI. |
| [!UICONTROL Numero massimo partecipanti] | `maxParticipants` | Intero | Numero massimo di partecipanti supportati, con un valore minimo di `0`. |
| [!UICONTROL Chiave sessione] | `sessionKey` | Stringa | Chiave di sessione richiesta dal servizio virtuale. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
