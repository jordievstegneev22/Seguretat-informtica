# Informe: Gestors de contrasenyes a EverPia

**Autor:** _Jordi Evstegneev_ · **Data:** 20/10/2026

## Índex

1. [Introducció i justificació](#1-introducció-i-justificació)
2. [Comparativa tècnica](#2-comparativa-tècnica)
3. [Avantatges i inconvenients](#3-avantatges-i-inconvenients)
4. [Recomanació](#4-recomanació)
5. [Fonts](#fonts)

## 1. Introducció i justificació

El problema d'EverPia va començar per una cosa molt simple: un compte tècnic tenia una contrasenya feble o repetida. Amb només aquesta contrasenya, els atacants van poder entrar i robar informació d'un projecte que encara s'estava fent. Per això la Direcció Tècnica vol que tothom faci servir un gestor de contrasenyes. Així cada compte tindrà la seva pròpia contrasenya i serà difícil d'endevinar.

### 1.1 Per què és tan perillós tenir contrasenyes febles o repetides

Hi ha molts tipus d'atacs que aprofiten les contrasenyes dolentes. Aquests són els més importants:

| Atac | Com funciona | Per què ens afecta |
| --- | --- | --- |
| Atac de diccionari | Un programa prova paraules normals, noms i variacions (per exemple Everpia2024! o Admin123) | Quan una persona s'inventa una contrasenya, normalment segueix patrons que es poden endevinar |
| Força bruta | El programa prova totes les combinacions de lletres, números i símbols | Una contrasenya de 8 caràcters es pot trencar en poques hores amb targetes gràfiques. Una de 20 caràcters a l'atzar, no |
| Credential stuffing | L'atacant agafa usuaris i contrasenyes que s'han filtrat d'altres webs i els prova als nostres sistemes | Si un tècnic fa servir la mateixa contrasenya en un fòrum que han hackejat i a la VPN de l'empresa, l'atacant entra sense haver de trencar res |
| Password spraying | Es proven poques contrasenyes molt típiques contra molts comptes diferents | Com que fa pocs intents per compte, no salta el bloqueig, i acaba trobant el compte més fluix |
| Phishing | T'enganyen perquè posis la contrasenya en una web falsa | Si aquella contrasenya la tens repetida, amb una sola víctima poden entrar a molts serveis |

El problema de fons és que les persones no podem recordar moltes contrasenyes llargues i rares. Per això la gent les fa curtes, fàcils o les repeteix. En un compte tècnic això és encara pitjor, perquè té més permisos i pot entrar a servidors, repositoris i dades dels clients.

### 1.2 Per a què serveix un gestor de contrasenyes

Un gestor de contrasenyes és com una caixa forta xifrada on guardes totes les contrasenyes. Només l'obres amb una contrasenya principal, que es diu contrasenya mestra. Ajuda de cinc maneres:

- **Contrasenyes úniques:** cada servei té la seva. Si se'n filtra una, les altres continuen segures (així s'evita el credential stuffing).
- **Contrasenyes fortes:** el generador fa contrasenyes a l'atzar de 20 caràcters o més. Amb diccionari o força bruta no es poden trencar.
- **No te les has de saber:** només has de recordar la contrasenya mestra.
- **Ajuda contra el phishing:** l'emplenament automàtic només funciona a la web correcta. Si estàs en una web falsa, no surt res.
- **Tot queda xifrat:** les contrasenyes es guarden xifrades amb AES-256, i no en un Excel, en notes o en un post-it.

Tot això va en la mateixa línia que el que recomana l'INCIBE sobre les contrasenyes a les empreses: que siguin llargues, que n'hi hagi una diferent per a cada servei i que es guardin amb eines segures.

## 2. Comparativa tècnica

Els dos programes xifren les dades amb AES-256 i els dos són de codi obert. La diferència més gran és on es guarda la base de dades i qui s'encarrega de sincronitzar-la.

| Criteri | Bitwarden (online / núvol) | KeePassXC (offline / escriptori) |
| --- | --- | --- |
| On es guarden les dades | En una caixa forta xifrada als servidors de Bitwarden. També es pot muntar en un servidor propi (self-hosting) | En un sol arxiu .kdbx a l'ordinador o a la unitat que triïs |
| Sincronització | Es fa sola i al moment entre tots els dispositius | No en té. L'arxiu s'ha de copiar a mà o amb un altre servei (Nextcloud, OneDrive, Syncthing) |
| Model de seguretat | Xifratge end-to-end i zero-knowledge: les dades es xifren al teu dispositiu abans d'enviar-les, i el servidor no veu mai la contrasenya mestra | L'arxiu es xifra en local. Ningú més en té còpia, però la seguretat depèn de l'usuari i del seu ordinador |
| Algoritmes | AES-256-CBC + HMAC. La clau es treu amb PBKDF2-SHA256 o Argon2id | AES-256, ChaCha20 o Twofish. La clau es treu amb Argon2 (format KDBX 4) |
| Autenticació | Contrasenya mestra + 2FA (app TOTP, correu o claus físiques com YubiKey) | Contrasenya mestra + arxiu clau (key file) si vols + YubiKey (challenge-response) si vols |
| Accés des de diferents dispositius | Windows, macOS, Linux, Android, iOS, web i extensions per als navegadors principals | Windows, macOS i Linux. Al mòbil cal una app d'una altra empresa que sigui compatible (KeePassDX, KeePassium, Strongbox) |
| Extensió del navegador | Oficial i funciona sola | KeePassXC-Browser. Només funciona si tens el programa d'escriptori obert |
| Codi obert | Sí (GPL/AGPL) i el revisen empreses externes cada cert temps (auditories) | Sí (GPL v3), el fa la comunitat |
| Depèn del núvol | Sí, menys si fas self-hosting | Gens |
| Portabilitat | Es pot exportar a JSON (xifrat o sense xifrar) i a CSV | L'arxiu .kdbx és estàndard: l'obre qualsevol programa compatible amb KeePass. També hi ha versió portable que no cal instal·lar |
| Gestió d'equips | Organitzacions, col·leccions compartides, registres d'activitat i polítiques (als plans de pagament) | No pot gestionar usuaris des d'un sol lloc. Es pot compartir un arxiu, però no pots posar permisos per a cada usuari |
| Preu | Freemium: gratis per a una persona. Premium 1,65 $/mes, Teams 4 $/usuari/mes i Enterprise 6 $/usuari/mes (pagant l'any sencer) | Totalment gratis |

Els preus els he mirat a la [pàgina oficial de Bitwarden](https://bitwarden.com/en-gb/pricing/) l'octubre de 2026. Estan en dòlars i sense impostos.

## 3. Avantatges i inconvenients

Resumint: l'opció online és més fàcil de fer servir i és millor perquè l'empresa no s'aturi si passa alguna cosa. L'opció offline et dona més control i no depens de ningú, però l'usuari ha de fer més feina.

| Aspecte | Online (Bitwarden) | Offline (KeePassXC) |
| --- | --- | --- |
| Seguretat: a favor | És zero-knowledge: encara que ataquin el servidor, només trobaran dades xifrades. Té 2FA i accepta claus físiques | No hi ha cap servidor de fora que es pugui atacar. L'usuari controla l'arxiu completament |
| Seguretat: en contra | Has de confiar en una empresa de fora, i com que té moltes dades és un objectiu molt buscat pels atacants | Si l'ordinador té un virus o l'arxiu es copia a llocs poc segurs, el risc és de l'usuari. No té 2FA de compte, només key file o YubiKey |
| Facilitat d'ús: a favor | Funciona igual a l'ordinador, al mòbil i al navegador i no s'ha de configurar res | És ràpid, lleuger i no cal crear cap compte ni registrar-se |
| Facilitat d'ús: en contra | Necessita Internet per sincronitzar (però guarda una còpia de la caixa forta a l'ordinador) | Sincronitzar entre dispositius s'ha de fer a mà. Al mòbil cal una altra app, i l'extensió només va amb el programa d'escriptori obert |
| Continuïtat de l'empresa: a favor | Si perds el portàtil o se t'espatlla, les contrasenyes continuen al núvol. Amb les organitzacions es poden recuperar comptes i compartir contrasenyes de l'equip | No depèn que l'empresa del programa continuï existint ni que els seus servidors funcionin |
| Continuïtat de l'empresa: en contra | Si el servei cau o l'empresa tanca, et pots quedar sense accés (això es pot evitar amb exportacions i self-hosting) | Si perds l'arxiu i no tens còpia, perds totes les contrasenyes. Si oblides la contrasenya mestra, no es pot recuperar de cap manera |

En els dos casos, la contrasenya mestra és el punt més dèbil: si la descobreixen, tenen accés a tot. Per això ha de ser llarga (una frase de 4 paraules o més), no s'ha de repetir enlloc i no s'ha d'apuntar enlloc.

## 4. Recomanació

Després de comparar les dues opcions, jo recomano **Bitwarden** per al personal tècnic d'EverPia, amb el pla Teams (4 $/usuari/mes) i amb el 2FA obligatori per a tothom.

Per què l'he triat:

1. **Soluciona el problema que va causar l'atac.** Com que se sincronitza sol i té extensió del navegador a tots els dispositius, és més còmode generar una contrasenya nova que repetir-ne una de vella. Si una eina costa de fer servir, al final la gent la deixa.
2. **No cal fiar-se de l'empresa de Bitwarden.** Com que és zero-knowledge i té xifratge end-to-end, si algú entra als seus servidors només trobarà dades xifrades. A més, el codi és obert i està auditat.
3. **Es pot gestionar l'equip.** Amb les organitzacions podem compartir les contrasenyes tècniques (servidors, routers, comptes de servei) en col·leccions amb permisos. Els registres d'activitat ens diuen qui ha entrat a què. Amb KeePassXC, si tot l'equip comparteix un arxiu, no es poden posar permisos ni saber qui ha fet què.
4. **L'empresa no s'atura.** Si es perd un portàtil, no es perden les contrasenyes. I si algú oblida la seva, es pot recuperar el compte i no es queda sense poder treballar.
5. **El preu es pot pagar.** El pla Teams costa molt menys que un sol atac com el que acabem de patir.

A més, s'han de fer aquestes coses sí o sí:

- Activar el 2FA al compte de Bitwarden de cada tècnic (amb app d'autenticació o clau física).
- Fer una contrasenya mestra de 4 paraules o més, que no es faci servir enlloc més.
- Fer una exportació xifrada de la caixa forta cada cert temps com a còpia de seguretat (està explicat a la [Guia d'Ús](02-Guia-Us-Bitwarden.md)).
- Canviar ara mateix totes les contrasenyes que estaven repetides, començant pels comptes tècnics.

Tot i així, KeePassXC continua sent una bona opció en alguns casos: per exemple, en ordinadors que no estan connectats a la xarxa o per a contrasenyes molt delicades que no han de sortir mai d'un ordinador.

## Fonts

- [Bitwarden: Password Manager Pricing & Plans](https://bitwarden.com/en-gb/pricing/) — preus i funcions per pla.
- INCIBE: Gestión de contraseñas seguras (enllaç de l'enunciat).
- INCIBE: Gestores de contraseñas: qué son y cómo pueden mejorar la seguridad de las empresas (enllaç de l'enunciat).
- [Documentació oficial de KeePassXC](https://keepassxc.org/docs/).
