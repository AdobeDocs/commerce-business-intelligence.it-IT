---
title: Connessione di MySQL tramite una connessione diretta
description: Scopri come connetterti [!DNL MongoDB] tramite connessione diretta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Connetti [!DNL MySQL] tramite connessione diretta

## In questo argomento

* [Consenti accesso a [!DNL Commerce Intelligence] Indirizzo IP](#allowlist)
* [Creare un [!DNL MySQL] utente per [!DNL Commerce Intelligence]](#steptwo)
* [Immetti le informazioni di connessione in [!DNL Commerce Intelligence]](#stepthree)

## Passa a

* [[!DNL MySQL] tramite ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] tramite [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] consiglia di utilizzare [SSH](../integrations/mysql-via-ssh-tunnel.md) o un&#39;altra forma di crittografia per proteggere i dati. Se questa non è un&#39;opzione, è comunque possibile connettersi direttamente [!DNL Commerce Intelligence] nel database seguendo le istruzioni riportate in questo argomento.

Questo argomento illustra come connettere direttamente [!DNL MySQL] database a [!DNL Commerce Intelligence]. Queste impostazioni possono essere utilizzate anche con [!DNL Adobe Commerce] o qualsiasi altro database di eCommerce che utilizza MySQL.

## Consenti accesso a [!DNL Commerce Intelligence] Indirizzi IP {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma è anche nel [!DNL MySQL] pagina credenziali:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creare un [!DNL MySQL] utente per [!DNL Commerce Intelligence]

Il modo più semplice per creare un’ `MySQL` utente per [!DNL Commerce Intelligence] : per eseguire la seguente query quando si accede a `MySQL` con `GRANT` privilegi. Sostituisci `Commerce Intelligence IP Address` con [!DNL Commerce Intelligence] Indirizzo IP e sostituzione `secure password` con una password sicura a tua scelta:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Per impedire all&#39;utente di accedere ai dati in database, tabelle o colonne specifici, è possibile eseguire `GRANT` query che consentono solo l&#39;accesso ai dati consentiti.

**Eseguire nuovamente la query GRANT per tutti gli IP richiesti utilizzando lo stesso utente e la stessa password.**

## Immetti le informazioni di connessione in Commerce Intelligence

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato il [!DNL MySQL] la pagina delle credenziali è aperta? In caso contrario, vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi fare clic su [!DNL MySQL] icona. Non dimenticare di modificare il `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, iniziando da `Database Connection` sezione:

* `Connection Nickname`: immetti un nome per l’integrazione (ad esempio, Archivio e-commerce)
* `Username`: nome utente per [!DNL Commerce Intelligence] [!DNL MySQL] utente
* `Password`: password per [!DNL Commerce Intelligence] [!DNL MySQL] utente
* `Port`: porta MySQL sul server (`3306` per impostazione predefinita)
* `Host`: per impostazione predefinita, è localhost. In generale, è il valore bind-address per il [!DNL MySQL] , che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

   Il valore si trova nella `my.cnf` file (che si trova in `/etc/my.cnf`) sotto la riga che recita `\[mysqld\]`. Se la riga dell&#39;indirizzo di associazione viene inserita come commento in tale file, il server viene protetto dai tentativi di connessione esterni.

Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Documentazione correlata

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
