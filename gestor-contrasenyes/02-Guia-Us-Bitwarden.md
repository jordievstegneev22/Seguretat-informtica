# Guia d'Ús Tècnica: Bitwarden

**Autor:** _(posa aquí el teu nom)_ · **Data:** 20/10/2026

Aquesta guia és per a l'equip tècnic d'EverPia. Explica pas a pas com instal·lar Bitwarden a Windows 11, com generar contrasenyes segures, com guardar les credencials, com fer servir l'emplenament automàtic i com fer còpies de seguretat.

## Índex

0. [Abans de començar](#abans-de-començar)
1. [Instal·lació i configuració inicial](#1-installació-i-configuració-inicial)
2. [Generació de contrasenyes segures](#2-generació-de-contrasenyes-segures)
3. [Desar credencials](#3-desar-credencials)
4. [Extensió del navegador i emplenament automàtic](#4-extensió-del-navegador-i-emplenament-automàtic)
5. [Còpies de seguretat](#5-còpies-de-seguretat)

## Abans de començar

Per seguir la guia necessites un ordinador amb Windows 11 i Internet, un navegador (Edge, Chrome o Firefox) i el mòbil amb una app d'autenticació (Google Authenticator, Microsoft Authenticator o una de semblant).

Totes les captures de pantalla estan fetes a la meva màquina virtual de Windows 11.

## 1. Instal·lació i configuració inicial

### 1.1 Crear el compte mestre

Primer s'ha de crear el compte a la web. Després, al programa només hi has d'iniciar sessió.

1. Obre el navegador i ves a `https://vault.bitwarden.eu`. Fem servir el servidor d'Europa perquè així les dades es queden a Europa i es compleix l'RGPD.

    ![Captura 1: pàgina d'inici de sessió de Bitwarden](img/captura01.png)

2. Clica **Crea un compte**, posa el correu de l'empresa i el teu nom i clica **Continua**.

3. T'arribarà un correu per verificar el compte. Obre'l i clica l'enllaç.
4. Ara has de posar la **contrasenya mestra**. Ha de tenir 12 caràcters com a mínim, però és millor fer una frase de 4 paraules o més (per exemple, una cosa com `cavall-bateria-grapa-correcte-27`). Posa també una pista que no doni la contrasenya.

    ![Captura 2: formulari de contrasenya mestra](img/captura02.png)

5. Clica **Crea un compte**. Ja tens la caixa forta (vault), encara buida.

> **Compte:** Bitwarden no et pot recuperar la contrasenya mestra. Si te l'oblides, perds l'accés a totes les teves dades.

### 1.2 Activar la verificació en dos passos (2FA)

1. A la caixa forta de la web, ves a **Configuració → Seguretat → Inici de sessió en dos passos**.
2. A l'apartat **Aplicació d'autenticació**, clica **Gestiona** i escriu la contrasenya mestra.
3. Amb l'app d'autenticació del mòbil, escaneja el codi QR i escriu el codi de 6 números que et surt.

    ![Captura 3: codi QR de l'aplicació d'autenticació](img/captura03.png)

4. Clica **Activa**.
5. Torna a la pantalla d'abans i clica **Mostra el codi de recuperació**. Apunta'l en un paper i guarda'l en un lloc segur.

    ![Captura 4: 2FA activat](img/captura04.png)

### 1.3 Instal·lar el programa a Windows 11

1. Ves a `https://bitwarden.com/download` i, a la part de **Desktop**, descarrega l'instal·lador de Windows.

    ![Captura 5: pàgina de descàrrega](img/captura05.png)

2. Obre l'arxiu `Bitwarden-Installer-x.x.x.exe` i ves fent l'instal·lador amb les opcions que surten per defecte.
3. També es pot instal·lar des del terminal (PowerShell) amb aquesta comanda:

```powershell

    winget install Bitwarden.Bitwarden
```

4. Obre Bitwarden. Abans d'iniciar sessió, al selector de servidor tria **bitwarden.eu** (el mateix on has creat el compte).
5. Inicia sessió amb el correu, la contrasenya mestra i el codi del 2FA.

    ![Captura 6: aplicació d'escriptori amb la caixa forta oberta](img/captura06.png)

### 1.4 Configuració que recomano

Ves a **Fitxer → Configuració** (o **Configuració** al menú) i canvia això:

- **Temps d'espera de la caixa forta:** 15 minuts.
- **Què fa quan s'acaba el temps:** Bloquejar.
- **Desbloquejar amb Windows Hello:** activa-ho si l'ordinador ho té, així no has d'escriure la contrasenya mestra cada vegada.
- **Esborrar el porta-retalls:** 30 segons. Així les contrasenyes que copies no s'hi queden guardades.

![Captura 7: pantalla de configuració](img/captura07.png)

## 2. Generació de contrasenyes segures

Cada vegada que facis un compte nou, la contrasenya l'ha de fer Bitwarden, no tu. Ha de tenir 20 caràcters a l'atzar amb majúscules, minúscules, números i símbols.

### 2.1 On trobar el generador

- **Al programa d'escriptori:** menú **Visualitza → Generador** (o prem `Ctrl+G`).
- **A l'extensió del navegador:** pestanya **Generador**.
- **Mentre crees un element:** al camp Contrasenya, clica la icona de les fletxes en cercle (Genera).

![Captura 8: finestra del generador](img/captura08.png)

### 2.2 Opcions del generador i què posar-hi


| Opció | Què fa | Què posem a l'equip tècnic |
| --- | --- | --- |
| Tipus | Contrasenya (caràcters a l'atzar) o Frase de pas (paraules) | Contrasenya |
| Longitud | Quants caràcters té (de 5 a 128) | 20 com a mínim. 32 per als comptes d'administrador i de servei |
| A-Z | Posa majúscules | Activat |
| a-z | Posa minúscules | Activat |
| 0-9 | Posa números | Activat |
| !@#$%^&* | Posa símbols | Activat (només el treus si el servei no accepta símbols) |
| Mínim de números | Assegura que hi hagi com a mínim aquests números | 2 |
| Mínim de caràcters especials | Assegura que hi hagi com a mínim aquests símbols | 2 |
| Evitar caràcters ambigus | Treu els caràcters que es confonen, com l, 1, O, 0 | Activat si la contrasenya s'ha de llegir o dir en veu alta |

**Frase de pas:** només la fem servir per a contrasenyes que s'han d'escriure a mà (com la mestra o la d'un ordinador on no hi ha el gestor). Posa-hi 5 paraules o més, el separador `-`, la primera lletra en majúscula i que hi hagi un número.

### 2.3 Pas a pas: fer una contrasenya i fer-la servir

1. Obre el generador i posa les opcions de la taula d'abans.
2. Clica la icona de **tornar a generar** fins que en surti una de nova.
3. Clica **Copia** o, si estàs creant un element, **Utilitza aquesta contrasenya**.
4. Guarda sempre l'element **abans** de canviar la contrasenya a la web o al servei. Així no la perds.

![Captura 9: generador amb les opcions recomanades](img/captura09.png)

### 2.4 Per què aquests valors

Una contrasenya de 20 caràcters triats entre uns 90 símbols té uns 130 bits d'entropia (l'entropia és com de difícil és d'endevinar). Amb els ordinadors d'ara, provar-les totes per força bruta és impossible. En canvi, una de 8 caràcters té uns 52 bits i es pot trencar en unes hores.

**Historial:** el generador guarda les últimes contrasenyes que has fet (icona del rellotge). Si en generes una i t'oblides de guardar-la, la pots recuperar d'allà.

## 3. Desar credencials


Cada credencial es guarda com un element del tipus **Inici de sessió**, amb nom, usuari, contrasenya i URL. L'URL és molt important, perquè sense ella no funciona l'emplenament automàtic.

### 3.1 Compte de correu electrònic

Exemple: el correu de l'empresa `tecnic@everpia.com`.

1. Al programa, clica **+** (Afegeix un element) i tria el tipus **Inici de sessió**.
2. Omple els camps:
    - **Nom:** Correu corporatiu EverPia
    - **Nom d'usuari:** tecnic@everpia.com
    - **Contrasenya:** clica la icona de generar (com a l'apartat 2) i accepta
    - **URI 1:** `https://outlook.office.com` (o la web del correu de l'empresa)
3. Si el compte té 2FA amb codis TOTP, enganxa la clau secreta al camp **Clau d'autenticació (TOTP)** (això només va amb Premium o amb un pla d'empresa).
4. Tria la **Carpeta** (fes-ne una que es digui `Correu`) i clica **Desa**.
5. Entra al correu i canvia la contrasenya vella per la que has generat.

![Captura 10: element del compte de correu desat](img/captura10.png)

### 3.2 Aplicació o servei web

Exemple: el panell d'administració d'un servidor o un compte de GitHub.

1. Clica **+** → **Inici de sessió**.
2. Omple els camps:
    - **Nom:** GitHub EverPia
    - **Nom d'usuari:** l'usuari d'aquest servei
    - **Contrasenya:** generada
    - **URI 1:** `https://github.com/login`
3. A l'opció de l'URI (icona de l'engranatge), deixa la detecció en **Domini base**. Si és un panell intern amb port (per exemple `https://192.168.1.10:8443`), tria **Amfitrió**.
4. Posa'l a la carpeta `Serveis web` i clica **Desa**.

![Captura 11: element del servei web desat](img/captura11.png)


### 3.3 Com ho recomano organitzar

- Una carpeta per a cada tipus: `Correu`, `Serveis web`, `Servidors`, `Xarxa`.
- Les contrasenyes que comparteix tot l'equip van a la **col·lecció** de l'organització, no a la caixa forta personal.
- Marca com a **Preferit** el que fas servir cada dia.

## 4. Extensió del navegador i emplenament automàtic

L'extensió posa l'usuari i la contrasenya només quan la web és la mateixa que tens guardada. Si entres a una web de phishing, no et proposarà res, i això ja t'avisa que alguna cosa no va bé.

### 4.1 Instal·lar l'extensió

1. Entra a `https://bitwarden.com/download` i, a **Browser extensions**, tria el teu navegador (Edge, Chrome o Firefox). També la pots trobar a la botiga d'extensions buscant "Bitwarden".
2. Clica **Afegeix a Edge / Chrome** i confirma.
3. Fixa la icona a la barra (icona del trencaclosques → fixar).
4. Obre l'extensió, tria el servidor **bitwarden.eu** i inicia sessió amb la contrasenya mestra i el 2FA.

![Captura 12: extensió instal·lada i fixada](img/captura12.png)

### 4.2 Configurar l'emplenament

A l'extensió, ves a **Configuració → Emplenament automàtic** i posa això:

- **Mostra suggeriments als camps del formulari:** activat (et surt un menú a sota dels camps d'usuari i contrasenya).
- **Emplenament automàtic en carregar la pàgina:** desactivat (és més segur que ho confirmis tu).
- **Demana per afegir inicis de sessió:** activat, perquè et pregunti si vols guardar les credencials noves.
- Desactiva el gestor de contrasenyes que porta el navegador (a Edge/Chrome: Configuració → Contrasenyes → "Oferir desar contrasenyes": desactivat). Així no tens dos gestors barallant-se.

![Captura 13: configuració d'emplenament](img/captura13.png)

### 4.3 Fer servir l'emplenament automàtic


Hi ha tres maneres d'omplir un formulari per iniciar sessió:

1. **Menú al camp:** clica al camp de l'usuari i tria la credencial al menú de Bitwarden que surt.
2. **Icona de l'extensió:** obre l'extensió i, a la pestanya de la pàgina on ets, et sortiran les credencials que coincideixen. Clica **Omple**.
3. **Drecera de teclat:** `Ctrl+Maj+L` omple la primera que coincideix.

![Captura 14: menú d'emplenament sobre el formulari de login](img/captura14.png)

### 4.4 Guardar una credencial nova des del navegador

Quan inicies sessió o et registres en una web que no tens guardada, Bitwarden et mostra una barra a dalt amb el botó **Desa**. Si el clices, la credencial es guarda amb l'URL correcta. Si canvies una contrasenya, et sortirà **Actualitza**.

![Captura 15: barra de desar credencial](img/captura15.png)

## 5. Còpies de seguretat

Cada tècnic ha de fer una exportació xifrada amb contrasenya un cop al mes, i guardar-la en un USB xifrat amb BitLocker que no estigui al costat de l'ordinador.

Encara que les dades ja estiguin al núvol, la còpia et salva si et quedes sense poder entrar al compte, si esborres alguna cosa sense voler o si el servei cau.

### 5.1 Tipus d'exportació

| Format | Està xifrat? | Quan s'ha de fer servir |
| --- | --- | --- |
| .json (Xifrat) — Protegit amb contrasenya | Sí, amb una contrasenya que poses tu | **És la còpia de seguretat que recomano.** Es pot importar a qualsevol compte de Bitwarden |
| .json (Xifrat) — Restringit al compte | Sí, amb la clau del teu compte | Només es pot importar al mateix compte. Si et quedes sense accés, no et serveix |
| .json | No | Per passar-te a un altre gestor. Mai per guardar-la com a còpia |
| .csv | No | Igual que l'anterior, i a més perd informació (carpetes, camps personalitzats) |

### 5.2 Pas a pas: fer l'exportació xifrada


1. Al programa d'escriptori, ves a **Fitxer → Exporta la caixa forta** (a la web és **Eines → Exporta la caixa forta**).
2. A **Exporta des de**, tria **La meva caixa forta**.
3. A **Format de fitxer**, tria **.json (Xifrat)**.
4. A **Tipus d'exportació**, tria **Protegit amb contrasenya**.
5. Posa una **contrasenya per a l'arxiu** que sigui llarga i diferent de la mestra, i torna-la a escriure. Guarda-la com un element dins de Bitwarden i també en un paper, al mateix lloc on tens el codi de recuperació del 2FA.
6. Clica **Confirma el format**, escriu la contrasenya mestra i guarda l'arxiu amb la data al nom: `bitwarden_backup_2026-10-20.json`.

![Captura 16: pantalla d'exportació amb les opcions marcades](img/captura16.png)

> **Compte:** l'exportació no guarda els arxius adjunts ni el que hi ha a la paperera. Els adjunts els has de descarregar a part.

### 5.3 On guardar la còpia

**La millor opció: un USB xifrat amb BitLocker To Go**

1. Connecta l'USB, ves a l'Explorador de fitxers, clica amb el botó dret a la unitat → **Activa BitLocker** (això surt a Windows 11 Pro i Enterprise).
2. Tria **Utilitza una contrasenya per desbloquejar la unitat** i posa'n una de forta.
3. Guarda la clau de recuperació de BitLocker (la pots imprimir o guardar a Bitwarden).
4. Tria **Xifra tota la unitat** i **Mode compatible**, i clica **Inicia el xifratge**.
5. Copia l'arxiu `.json` a l'USB i esborra'l de la carpeta Baixades.
6. Guarda l'USB en un lloc segur (un calaix amb clau o una caixa forta), però mai al costat del portàtil.

![Captura 17: unitat USB amb BitLocker activat](img/captura17.png)

**Una opció de més: el núvol xifrat.** També pots pujar una segona còpia al núvol de l'empresa (OneDrive o Nextcloud) dins d'un contenidor xifrat (VeraCrypt o un arxiu 7-Zip amb AES-256). Com que l'exportació ja està xifrada, així tens dues capes de protecció.

Això segueix la **regla 3-2-1**: 3 còpies (el núvol de Bitwarden, l'USB i el núvol de l'empresa), en 2 llocs de tipus diferent, i 1 fora de l'oficina.

### 5.4 Recuperar una còpia

1. Inicia sessió a la caixa forta de la web i ves a **Eines → Importa dades**.
2. Tria el format **Bitwarden (json)** i selecciona l'arxiu.

3. Posa la contrasenya de l'arxiu i clica **Importa**.

Prova de recuperar la còpia com a mínim una vegada en un compte de proves. Si una còpia no s'ha provat mai, no saps si funcionarà.

### 5.5 Errors que s'han d'evitar

- Deixar exportacions sense xifrar (`.csv` o `.json`) a Baixades, a l'escriptori o al correu.
- Posar la contrasenya mestra com a contrasenya de l'arxiu.
- Portar l'USB amb la còpia a la mateixa motxilla que el portàtil.
