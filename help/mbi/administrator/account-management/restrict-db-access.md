---
title: Limitazione dell’accesso al database
description: Scopri come limitare l’accesso, limitando l’accesso al server che ospita il database.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Limita l’accesso

Quando si crea un tunnel SSH sul server, non è necessario [!DNL Adobe Commerce Intelligence] per avere accesso a qualsiasi elemento diverso dal database. Se non vuoi [!DNL Commerce Intelligence] per avere accesso completo al server che ospita il database, è possibile limitare l&#39;accesso forzando [!DNL Commerce Intelligence Linux] utente in un [shell bash con restrizioni](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

È possibile indovinare dal nome, ma viene utilizzata una shell base limitata per impostare un ambiente più controllato della shell standard. La cosa importante di questo tipo di shell è che gli utenti con restrizioni della shell non possono accedere alle funzioni di sistema né apportare alcun tipo di modifica.

Per limitare [!DNL Commerce Intelligence Linux] utente, è necessario eseguire due operazioni:

1. Modifica la variabile di ambiente PATH in modo che sia la stringa vuota. Ciò significa che l&#39;utente non può accedere ai file eseguibili di sistema.

1. Assicurati che la shell eseguita sia `bash -r`

Entrambe queste operazioni possono essere eseguite all&#39;interno del `authorized_keys` file nella home dell’utente `dir/.ssh` come parte del comando eseguito quando l’utente effettua l’accesso. Ha un aspetto simile al seguente:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Al termine, l’utente creato per [!DNL Commerce Intelligence] non può apportare modifiche al sistema.
