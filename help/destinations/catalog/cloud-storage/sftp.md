---
keywords: SFTP;sftp
title: SFTP connection
description: Create a live outbound connection to your SFTP server to periodically export delimited data files from Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 99bb5d1b76b926622ca21fa1df7c3cb9fabc4856
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# SFTP connection

## Panoramica {#overview}

Create a live outbound connection to your SFTP server to periodically export delimited data files from Adobe Experience Platform.

>[!IMPORTANT]
>
> [!DNL Amazon S3][!DNL Azure Blob]

## Export type and frequency {#export-type-frequency}

Refer to the table below for information about the destination export type and frequency.

| Elemento | Tipo | Note |
---------|----------|---------|
| Export type | **** | [](../../ui/activate-batch-profile-destinations.md#select-attributes) |
| Export frequency | **** | Batch destinations export files to downstream platforms in increments of three, six, eight, twelve, or twenty-four hours. [](/help/destinations/destination-types.md#file-based) |

{style=&quot;table-layout:auto&quot;}

![](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connect to the destination {#connect}

[](../../ui/connect-destination.md)

### Connection parameters {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA public key"
>abstract="Optionally, you can attach your RSA-formatted public key to add encryption to your exported files. Your public key must be written as a Base64 encoded string."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="SSH key"
>abstract="The SSH key requires a Base64 string."

[](../../ui/connect-destination.md)

#### Authentication information {#authentication-information}

****

![](../..//assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* ****
* ****
* ****
* **** [!DNL Base64]
   * Esempio: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`

      ![](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


****

![](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* ****
* ****
* ****
* ****
* **** [!DNL Base64]
   * Esempio: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`

      ![](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Destination details {#destination-details}

After establishing the authentication connection to the SFTP location, provide the following information for the destination:

![](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* ****
* ****
* ****

## Exported data {#exported-data}

[!DNL SFTP]`.csv` [](../../ui/activate-batch-profile-destinations.md)

## IP address allow list

[](ip-address-allow-list.md)
