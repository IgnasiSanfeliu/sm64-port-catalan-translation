# Super Mario 64 Port - Traducció al Català
#### [*Info in Catalan, to read the English version please click here.*](https://github.com/Nilcm01/sm64-port-catalan-translation#super-mario-64-port---catalan-translation)

La traducció catalana de Super Mario 64 ha estat creada per a portar el joc a un nou idioma emprant el Port de la Decompilació de SM64, per a que sigui jugable a tots els sistemes que es vulgui.
Aquest projecte **no** està relacionat, de cap manera, amb els equips responsables del Projecte de Decompilació ni del Port.

Els continguts, informació i instruccions del Port de SM64 estan detallats a continuació:

- Aquest repositori conté l'íntegra decompilació de Super Mario 64 (J), (U) i (E) amb excepcions menors al subsistema d'àudio.
- Les nomenclatures i documentació del codi font i de les estructures de dades estan encara en procés.
- Els esforços per a decompilar la ROM Shindou avança constantment a una construcció parella.
- A part de la Nintendo 64, també pot córrer nativament a Windows i Linux.

Aquest repositori no inclou totes les llibreries necessàries per a compilar el joc.
Es requereix una còpia prèvia del joc (ROM) per a extreure'n les llibreries. Aquesta ROM ha de ser del següent tipus:

- Regió: **U** o **US** (Estats Units).
- Extensió: .z64
- *Exemple: Super Mario 64 (U).z64*

**IMPORTANT**: De moment, l'única regió testada és la U/US; per tant, si us plau empreu aquesta versió per a assegurar que la traducció s'implementa adequadament.

## Llançaments

Per descarregar la darrera versió funcional si us plau consulteu aquest enllaç i després seguiu les instruccions detallades a baix:

https://github.com/Nilcm01/sm64-port-catalan-translation/releases

Per a més informació sobre els llençaments si us plau consulteu aquesta pàgina:

https://nilcm01.blogspot.com/2020/09/SM64PC-CAT.html

## Construir executables nadius

### Linux

1. Instal·lar els prerequisits (Ubuntu): `sudo apt install -y git build-essential pkg-config libusb-1.0-0-dev libsdl2-dev`.
2. Clona el respositori: `git clone https://github.com/Nilcm01/sm64-port-catalan-translation.git`, el qual crearà el directori `sm64-port-catalan-translation`, llavors **insereix** `cd sm64-port-catalan-translation`.
3. Col·loca una ROM de Super Mario 64 anomenada `baserom.us.z64` al directori arrel del repositori.
4. Empra `make` per a construir-la. Qualifica la versió a partir de `make VERSION=us`. Afegeix `-j4` per a millorar la velocitat de construcció (basat en el nombre de nuclis disponibles del processador).
5. El binari de l'executable es trobarà a `build/us_pc/sm64.us.f3dex2e`.

### Windows

1. Instal·la i actualitza MSYS2, seguint tots els passos llistats a https://www.msys2.org/.
2. Des del menú d'inici, executa MSYS2 MinGW i instal·la els paquets requerits depenent del teu sistema ( **NO** executis "MSYS2 MSYS"):
  * 64-bit: Executa "MSYS2 MinGW 64-bit" i instal·la: `pacman -S git make python3 mingw-w64-x86_64-gcc`
  * 32-bit (també funciona en sistemes de 64-bits): Executa "MSYS2 MinGW 32-bit" i instal·la: `pacman -S git make python3 mingw-w64-i686-gcc`
  * **NO** instal·lis per error el paquet anomenat simplement `gcc`.
3. El terminal d'MSYS2 té un _current working directory_ (directori actual de treball) que inicialment és `C:\msys64\home\<username>` (directori d'usuari). A la finestra de comandes veuràs el directori de treball actual de color groc. `~` és un àlies per a directori d'usuari. Pots canviar el directori actual de treball a `Documents` usant `cd /c/Users/<username>/Documents`.
4. Clona el repositori: `git clone https://github.com/Nilcm01/sm64-port-catalan-translation.git`, el qual crearà el directori `sm64-port-catalan-translation`, llavors **insereix** `cd sm64-port`.
5. Col·loca una ROM de *Super Mario 64* anomenada `baserom.us.z64` al directori arrel per a l'extracció de les llibreries.
6. Empra `make` per a construir-la. Qualifica la versió a partir de `make VERSION=us`. Afegeix `-j4` per a millorar la velocitat de construcció (basat en el nombre de nuclis del processador disponibles).
7. El binari de l'executable es trobarà a `build/us_pc/sm64.us.f3dex2e.exe` dins del repositori.

#### Resolució de problemes

1. Si reps `make: gcc: command not found` o `make: gcc: No such file or directory` encara que els paquets s'hagin instal·lat adequadament, probablement hagis executat el MSYS2 erroni. Llegeix les instruccions de nou. El terminal ha d'incloure "MINGW32" o "MINGW64" en text lila, i **NO** "MSYS".
2. Si reps `Failed to open baserom.us.z64!` has errat col·locant la ROM base al repositori. Pots escriure `ls` per a llistar tots els arxius al directori actual de treball. Si et trobes al directori `sm64-port-catalan-translation`, comprova que hi és allà.
3. Si reps `make: *** No targets specified and no makefile found. Stop.`, no ets al directori adequat. Comrpova que el text en groc al terminal finalitza amb `sm64-port-catalan-translation`. Utilitza `cd <dir>` per a introduir el directori correcte. Si escrius `ls` hi apareixeran tots els arxius del projecte, incloent-hi `Makefile` si tot és correcte.
4. Si reps cap error, comprova que els paquets d'MSYS2 estan actualitzats executant `pacman -Syu` i `pacman -Su`. Si la finestra d'MSYS2 es tanca immediatament reinicia el teu ordinador.
5. Quan executis `gcc -v` comprova que hi és `Target: i686-w64-mingw32` o `Target: x86_64-w64-mingw32`. Si veus `Target: x86_64-pc-msys`, has obert el menú d'inici d'MSYS erroni o has instal·lat el paquet de gcc erroni.

### Debugging

El codi pot ser debugat emprant `gdb`. A Linux instal·la el paquet `gdb`i executa `gdb <executable>`. A MSYS2 instal·la-ho executant `pacman -S winpty gdb` i executant `winpty gdb <executable>`. El programa `winpty` s'assegura que el teclat funciona adequadament al terminal. Considera també canviar el criteri d'execució (flag) `-mwindows` per `-mconsole` tant per a poder veure el "stdout/stderr" com per a poder prèmer CTRL+C per a interrompre el programa. Al "Makefile", assegura't que compiles les fonts emprant `-g` enlloc de `-O2` per a incloure símbols de debugging. Cerca un tutorial online per a utilitzar gdb.

## Construcció de la ROM 

També és possible construir ROMs de Nintendo 64 amb aquest repositori. Dirigeix-te a https://github.com/n64decomp/sm64 per instruccions.

## Estructura del projecte

```
sm64
├── actors: comportament d'ojectes, disposició dels terrenys, les llistes de visualització
├── asm: codi assembly escrit a mà, capçalera (header) de la rom
│   └── non_matchings: asm per a seccions no coincidents
├── assets: animacions i dades de prova
│   ├── anims: dades d'animacions
│   └── demos: dades de prova
├── bin: arxius en C per a endreçar llistes de visualització i textures
├── build: directori de sortida
├── data: scripts de comportament, dades miscel·lànies
├── doxygen: documentació de la infraestructura
├── enhancements: exemples de modificacions del codi font
├── include: arxius de capçalera
├── levels: scripts de nivells, disposició dels terrenys, llistes de visualització
├── lib: codi de la lliberira SDK
├── rsp: codi assembly de l'àudio i de Fast3D RSP
├── sound: sequüències, mostres (samples) de so, i bancs de sons
├── src: codi font en C del joc
│   ├── audio:  codi de l'àudio
│   ├── buffers: "stacks", "heaps", i buffers de tasques
│   ├── engine: motors de processament d'scripts i útils
│   ├── game: font dels comportaments de la resta del joc
│   ├── goddard: pantalla intrductoria de Mario
│   ├── menu: pantalla de títol i arxius, missions, i menus de sel·lecció de nivells de debug
│   └── pc: codi del port, renderitzador d'àudio i vídeo
├── text: diàlogs, noms de nivells, noms de missions
├── textures: caixa del cel (skybox) i dades de textures genèriques
└── tools: eines de construcció de l'executable
```

## Contribuir-hi

Les "Pull requests" són benvingudes. Per canvis majors, obriu primer si us plau obriu primer una "issue" per a discutir que voldriueu canviar.

Executa `clang-format` al vostre codi per a assegurar-vos que compleix els estàndards de codi del projecte.

Contacte del projecte de traducció: https://twitter.com/PelochoRockea

Discord oficial del projecte: https://discord.gg/7bcNTPK


# Super Mario 64 Port - Catalan Translation
#### [*Informació en anglès, per a llegir la versió catalana si us plau cliqueu aquí.*](https://github.com/Nilcm01/sm64-port-catalan-translation#super-mario-64-port---traducci%C3%B3-al-catal%C3%A0)

The Super Mario 64 Catalan translation is created to bring the game to a new language using the SM64 Decompilation Port, so it is playable on all systems wanted.
This project is **not** related, by any means, to the original Decompilation Project nor Port teams.

The contents, info and instructions of the SM64 Port are detailed below:

- This repo contains a full decompilation of Super Mario 64 (J), (U), and (E) with minor exceptions in the audio subsystem.
- Naming and documentation of the source code and data structures are in progress.
- Efforts to decompile the Shindou ROM steadily advance toward a matching build.
- Beyond Nintendo 64, it can also target Linux and Windows natively.

This repo does not include all assets necessary for compiling the game.
A prior copy of the game (ROM) is required to extract the assets. This ROM has to be like this:

- Region: **U** o **US** (United States).
- Extension: .z64
- *Exemple: Super Mario 64 (U).z64*

**IMPORTANT**: By now, the only region tested is U/US, so please use this version to ensure that the translation applies successfully.

## Releases

To download the latest working release please refer to this link and then follow the instructions detailed below:

https://github.com/Nilcm01/sm64-port-catalan-translation/releases

For more information on the releases please check this link:

https://nilcm01.blogspot.com/2020/09/SM64PC-CAT.html

## Building native executables

### Linux

1. Install prerequisites (Ubuntu): `sudo apt install -y git build-essential pkg-config libusb-1.0-0-dev libsdl2-dev`.
2. Clone the repo: `git clone https://github.com/Nilcm01/sm64-port-catalan-translation.git`, which will create a directory `sm64-port-catalan-translation` and then **enter** it `cd sm64-port-catalan-translation.git`.
3. Place a Super Mario 64 ROM called `baserom.us.z64` into the repository's root directory for asset extraction.
4. Run `make` to build. Qualify the version through `make VERSION=us`. Add `-j4` to improve build speed (hardware dependent based on the amount of CPU cores available).
5. The executable binary will be located at `build/us_pc/sm64.us.f3dex2e`.

### Windows

1. Install and update MSYS2, following all the directions listed on https://www.msys2.org/.
2. From the start menu, launch MSYS2 MinGW and install required packages depending on your machine (do **NOT** launch "MSYS2 MSYS"):
  * 64-bit: Launch "MSYS2 MinGW 64-bit" and install: `pacman -S git make python3 mingw-w64-x86_64-gcc`
  * 32-bit (will also work on 64-bit machines): Launch "MSYS2 MinGW 32-bit" and install: `pacman -S git make python3 mingw-w64-i686-gcc`
  * Do **NOT** by mistake install the package called simply `gcc`.
3. The MSYS2 terminal has a _current working directory_ that initially is `C:\msys64\home\<username>` (home directory). At the prompt, you will see the current working directory in yellow. `~` is an alias for the home directory. You can change the current working directory to `My Documents` by entering `cd /c/Users/<username>/Documents`.
4. Clone the repo: `git clone https://github.com/Nilcm01/sm64-port-catalan-translation.git`, which will create a directory `sm64-port-catalan-translation` and then **enter** it `cd sm64-port-catalan-translation.git`.
5. Place a *Super Mario 64* ROM called `baserom.us.z64` into the repository's root directory for asset extraction.
6. Run `make` to build. Qualify the version through `make VERSION=us`. Add `-j4` to improve build speed (hardware dependent based on the amount of CPU cores available).
7. The executable binary will be located at `build/us_pc/sm64.us.f3dex2e.exe` inside the repository.

#### Troubleshooting

1. If you get `make: gcc: command not found` or `make: gcc: No such file or directory` although the packages did successfully install, you probably launched the wrong MSYS2. Read the instructions again. The terminal prompt should contain "MINGW32" or "MINGW64" in purple text, and **NOT** "MSYS".
2. If you get `Failed to open baserom.us.z64!` you failed to place the baserom in the repository. You can write `ls` to list the files in the current working directory. If you are in the `sm64-port-catalan-translation` directory, make sure you see it here.
3. If you get `make: *** No targets specified and no makefile found. Stop.`, you are not in the correct directory. Make sure the yellow text in the terminal ends with `sm64-port-catalan-translation`. Use `cd <dir>` to enter the correct directory. If you write `ls` you should see all the project files, including `Makefile` if everything is correct.
4. If you get any error, be sure MSYS2 packages are up to date by executing `pacman -Syu` and `pacman -Su`. If the MSYS2 window closes immediately after opening it, restart your computer.
5. When you execute `gcc -v`, be sure you see `Target: i686-w64-mingw32` or `Target: x86_64-w64-mingw32`. If you see `Target: x86_64-pc-msys`, you either opened the wrong MSYS start menu entry or installed the incorrect gcc package.

### Debugging

The code can be debugged using `gdb`. On Linux install the `gdb` package and execute `gdb <executable>`. On MSYS2 install by executing `pacman -S winpty gdb` and execute `winpty gdb <executable>`. The `winpty` program makes sure the keyboard works correctly in the terminal. Also consider changing the `-mwindows` compile flag to `-mconsole` to be able to see stdout/stderr as well as be able to press Ctrl+C to interrupt the program. In the Makefile, make sure you compile the sources using `-g` rather than `-O2` to include debugging symbols. See any online tutorial for how to use gdb.

## ROM building

It is possible to build N64 ROMs as well with this repository. See https://github.com/n64decomp/sm64 for instructions.

## Project Structure

```
sm64
├── actors: object behaviors, geo layout, and display lists
├── asm: handwritten assembly code, rom header
│   └── non_matchings: asm for non-matching sections
├── assets: animation and demo data
│   ├── anims: animation data
│   └── demos: demo data
├── bin: C files for ordering display lists and textures
├── build: output directory
├── data: behavior scripts, misc. data
├── doxygen: documentation infrastructure
├── enhancements: example source modifications
├── include: header files
├── levels: level scripts, geo layout, and display lists
├── lib: SDK library code
├── rsp: audio and Fast3D RSP assembly code
├── sound: sequences, sound samples, and sound banks
├── src: C source code for game
│   ├── audio: audio code
│   ├── buffers: stacks, heaps, and task buffers
│   ├── engine: script processing engines and utils
│   ├── game: behaviors and rest of game source
│   ├── goddard: Mario intro screen
│   ├── menu: title screen and file, act, and debug level selection menus
│   └── pc: port code, audio and video renderer
├── text: dialog, level names, act names
├── textures: skybox and generic texture data
└── tools: build tools
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Run `clang-format` on your code to ensure it meets the project's coding standards.

Translation project contact: https://twitter.com/PelochoRockea

Official project Discord: https://discord.gg/7bcNTPK
