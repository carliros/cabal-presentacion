CABAL
=====

"La facilidad de instalacion puede facilmente incrementar la adopcion de software en los usuarios destinos"

Concepto
========
Haskell Cabal es una arquitectura para constuir e instalar cualquier herramienta desarrollada en Haskell.

Este especifica una interfaz de linea de comandos que hace sencilla su construccion e instalacion de
librerias y aplicaciones para los usuarios finales.
Tambien provee herramientas para los creadores, los cuales implementan la interface de ocmandos atraves
de una libreria.

Paquete: Cualquier codigo fuente, libreria, documentacion o ejecutable para una distrubucion
Paquete Cabal: Es un colleccion de modulos Haskell que estan descritos por descripciones Cabal.
    Una descricion Cabal consiste de 2 archivos:
        * <PackageName>.cabal     => Archivo de descripcion declarativo, independiente del compilador
        * Setup.lhs [Setup.hs]    => Script de confifuracion

Un paquete puede incluir
    - liibrerias
    - ejecutables
    - ambos
Normalmente los paquetes son distribuidos en formato compreso con tar y gzip


Otros manejadores de paquete
============================
Ejemplos de otros manejadores de paquetes de sistemas operativos: rpm [red hat], dpkg [debian]

-- Make es una herramienta unix/linux que determina que partes del proyecto necesitan ser recompilados
-- tambien guarda los comandos para recompilarlos.
-- Direfencias Make y cabal
--      Cabal tiene descripcion del paquete y comandos pero Make es solo comandos
--      Make solo corre en unix-like, pero Cabal es donde sea existe haskell
--      Cabal hace un analisis de dependencia de paquetes instalados, y solo instala lo necesario
--      Cabal provee type-safe y abstracciones de alto nivel
-- Cosas: Pero la mayoria utiliza make en el proceso de construccion de sus librerias
-- y utilizan cabal para redistribuir el paquete
-- make presenta una serie de problemas cuando se intenta construir una arquitectura reusable

-- HMake es una herramienta inteligente de administracion de compilacion para programas de Haskell.
-- Parecido a Make.
-- Pero no se usa para empaquetar codigo haskell.

Detalles
========
    * cabal provee un "simple build infrastructure" el cual se usa para configurar, compilar, e instalar paquetes hakell
    * cabal provee 2 interfaces PARA LOS AUTORES (Los CREAN el paquete):
        - CLI para construir herramientas por capas
        - API que procee acceso para el Simple Build Interface.


Archivo Paquete de Descripcion :: <PackageName>.cabal
==============================
* Guarda informacion acerca de:
    - Como construir el paquete
    - Informacion Meta-Data usable para los usuarios finales, y bases de datos de paquetes.
* Es independiente del compilador
* Este archivo es el paquete de decripcion en el Cabal API
Debe existir informacion unica:
    - nombre
    - version
    - descripcion

Ejemplo de descripcion de paquete: pkgName.cabal
================================================
Name                : pkgName
Version             : 1.0
Build-Depends       : OtherPackage >= 1.1
Copyright           : (c) 2005 Isaac Jones
License             : BSD3
Maintainer          : Isaac Jones
Synopsis            : Brief description.
Exposed-Modules     : MyPackage
Other-Modules       : MyPackage.SubModule,
                      MyPackage.OtherModule
C-Sources           : cfile1.c, c_src/cfile2.c
Extensions          : ForeignFunctionInterface
Executable packageExe
    Main-is         : Main.hs
    Other-Modules   : MyPackage
    Extensions      : OverlappingInstances


A helpful error
===============
Fields allowed in "Description" section:
      name
    , version
    , cabal-version
    , build-type
    , license
    , license-file
    , copyright
    , maintainer
    , build-depends
    , stability
    , homepage
    , package-url
    , bug-reports
    , synopsis
    , description
    , category
    , author
    , tested-with
    , data-files
    , data-dir
    , extra-source-files
    , extra-tmp-files

Fields allowed in "Executable" section:
      executable
    , main-is
    , buildable
    , build-tools
    , cpp-options
    , cc-options
    , ld-options
    , pkgconfig-depends
    , frameworks
    , c-sources
    , extensions
    , extra-libraries
    , extra-lib-dirs
    , includes
    , install-includes
    , include-dirs
    , hs-source-dirs
    , other-modules
    , ghc-prof-options
    , ghc-shared-options
    , ghc-options
    , hugs-options
    , nhc98-options
    , jhc-options

Fields allowed in "Library" section:
      exposed-modules
    , exposed
    , buildable
    , build-tools
    , cpp-options
    , cc-options
    , ld-options
    , pkgconfig-depends
    , frameworks
    , c-sources
    , extensions
    , extra-libraries
    , extra-lib-dirs
    , includes
    , install-includes
    , include-dirs
    , hs-source-dirs
    , other-modules
    , ghc-prof-options
    , ghc-shared-options
    , ghc-options
    , hugs-options
    , nhc98-options
    , jhc-options

Distribution quality warnings:
    No 'category' field.
    No 'synopsis' field.
    Warning: Cannot run preprocessors. Run 'configure' command first.
    Building source dist for SimpleLenguajeLogo-1.1...
    Source tarball created: dist/SimpleLenguajeLogo-1.1.tar.gz


Herramienta cabal
=================
-> cabal init
Package name [default "carlos"]?
Package version [default "0.1"]?
Please choose a license:
   1) GPL
   2) GPL-2
   3) GPL-3
   4) LGPL
   5) LGPL-2.1
   6) LGPL-3
 * 7) BSD3
   8) BSD4
   9) MIT
  10) PublicDomain
  11) AllRightsReserved
  12) OtherLicense
  13) Other (specify)
Your choice [default "BSD3"]?
Author name? carlos
Maintainer email? carlos@gmail.com
Project homepage/repo URL? comunidadhaskell.org
Project synopsis? test de cabal init
Project category:
   1) Codec
   2) Concurrency
   3) Control
   4) Data
   5) Database
   6) Development
   7) Distribution
   8) Game
   9) Graphics
  10) Language
  11) Math
  12) Network
  13) Sound
  14) System
  15) Testing
  16) Text
  17) Web
  18) Other (specify)
Your choice? 18
Please specify? CabalTest
What does the package build:
   1) Library
   2) Executable
Your choice? 2
Generating LICENSE...
Generating Setup.hs...
Generating hcal.cabal...

You may want to edit the .cabal file and add a Description field.


Comando: runhaskell Setup.hs sdist
==================================
Se debe ejecutar en el siguiente orden
    1.- runhaskell Setup.hs configure
    2.- runhaskell Setup.hs sdist


Command Line Interface (CLI)
============================
    - Es una interface de alto nivel que esta encima de Cabal.
    - El CLI ayuda a los usuarios finales a instalar paquetes al simple vuelo (muy sencillo)
    - Se puede construir herramientas que trabajen sobre la CLI

Por ejemplo:
    setupCmd c = system ("./Setup.lhs " ++ c)
    main = do [package] <- getArgs
              download "http://packages.haskell.org/" package
              unpack package
              changeDirectory package
              setupCmd "configure --prefix=/usr/local"
              setupCmd "build"
              setupCmd "install"

**** Todo paquete Setup.hs/Setup.lhs es garantizado que tenga
        - configure --> prepara para contruir
        - buid      --> prepara para su instalacion
        - install   --> copia los archivos compilador en la maquina del
                        usuario final y SI EXISTE una LIBRERIA lo registra en el compilador
        - copy      --> copia los archivos en el directorio de instalacion,
                        igual que "install" pero no registra ningina libreria.
        - register  --> registra una libreria en el compilador
        - clean     --> limpia todo lo que se genera en el build
  -> Esto es gracias a Setup.lhs [Setup.hs]
  -> Muchos de los comandos tiene pueden tener argumentos para modificar su comportamiento
     Por ejemplo: --user    :: usar los paquetes genericos o los del usuario

      Ejemplo:  runhaskell Setup.hs configure
                runhaskell Setup.hs build
                runhaskell Setup.hs haddock
                runhaskell Setup.hs install


Simple Build Infraestructure
============================
    * Provee una infraestructura sencilla para el usuario: configure, build, install, ...
    * Facilita el trabajo el creador de paquete a simplemente especificar
      parametros de configuracion, y te libera de crear una lista de comandos a ejecutar (caso Makefile)
    * descripcion de estructura:
        - configure     localiza el compilador u otros paquetes necesarios para su compilacion
                        si se necesita una configuracion compleja: se puede usar autoconf (revizar mas del tema)
        - build         ejecuta los preprocesadores y nomrmalmente compila el codigo fuente
                        Cabal conoce que argumentos enviar en cada compilador (gracias al Setup.hs)
        - install       copia los archivos generados a la caperta de instalacion
                        y registra las librerias

        -OPCIONALES: * haddock      --> documentacion   
                     * hscolour     --> coloreado de sintaxis en la documentacion

runhaskell Setup.hs --help
==========================
This Setup program uses the Haskell Cabal Infrastructure.
See http://www.haskell.org/cabal/ for more information.

Usage: Setup.hs COMMAND [FLAGS]
   or: Setup.hs [GLOBAL FLAGS]

Global flags:
 -h --help            Show this help text
 -V --version         Print version information
    --numeric-version Print just the version number

Commands:
  configure     Prepare to build the package.
  build         Make this package ready for installation.
  install       Copy the files into the install locations. Run register.
  copy          Copy the files into the install locations.
  haddock       Generate Haddock HTML documentation.
  clean         Clean up after a build.
  sdist         Generate a source distribution file (.tar.gz).
  hscolour      Generate HsColour colourised code, in HTML format.
  register      Register this package with the compiler.
  unregister    Unregister this package with the compiler.
  test          Run the test suite, if any (configure with UserHooks).
  help          Help about commands

For more information about a command use
  Setup.hs COMMAND --help

Typical steps for installing Cabal packages:
  Setup.hs configure
  Setup.hs build
  Setup.hs install


El archivo Setup.hs/Setup.lhs
=============================

Ejemplo Setup.lhs
    #!/usr/bin/env runhaskell

    > import Distribution.Simple(defaultMain)
    > main = defaultMain

* A simple implementation of main for a Cabal setup script.
  It reads the package description file using IO, and performs the
  action specified on the command line. Ver documentacion:  libraries/Cabal-1.8.0.6/Distribution-Simple.html
* This module isn't called "Simple" because it's simple.
  Far from it. It's called "Simple" because it does complicated things to simple software.
* El "defaultMain" implementa el CLI basico para la compatibilidad.
* Setup.lhs puede ejecutar cualquier accion que el creador quiera usar siempre y cuando este conforme al CLI
  Esto significa que paquetes bien complejos, o tambien otro tipo de paquetes pueden estar envueltos en un
  nuevo modulo Setup
* DETALLE: It parses commands and options entered by the end-user and executes operations like configure,build, and install

## Distribution.Simple ##
- "DefaultMainWithHooks"
  Tiene un sistema flexible para extensiones, UserHook ==>> Gancho del usuario creador  === Arquitectura de Plugins  == eso lo hace extensible
  Los hooks te permiter configurar preprocesadores antes y despues de la compilacion
        defaultMainWithHooks :: UserHooks -> IO ()
        data UserHooks = UserHooks {
                            hookedPreProcessors :: [ PPSuffixHandler ]      {- ˆCustom preprocessors in addition to and overriding built-in preprocessors -}
                            -- | Hook to run before configure
                            ,preConf :: Args -> ConfigFlags -> IO HookedBuildInfo
                            -- | Hook to run after configure
                            ,postConf :: Args -> ConfigFlags -> LocalBuildInfo -> IO ExitCode ...
                         }


API
===
Existem varios, desde el mas simple hasta complejos o al reves.
Ver documentacion: Cabal/Distribution/...
    El mas usado Distribution.Simple


Layered Tools
=============
Son herramientas que trabajan sobre el CLI, API, o el meta-data de un paquete de Cabal.
Ejemplos: hackage, cabal-get

HackageDB
---------
Es la base de datos de paquetes de Haskell.
Un usuario puede subir un paquete a hackage, y hackage parsea su meta-data (descripcion)
con el API de Cabal y guarda la informacion en su base de datos y ademas provee una interfaz
web para usuarios finales que quieran usar el paquete, tambien guar el paquete en su servidor
para que lo puedan descargar.

Tambien proevee una interface XML-RPC, de manera que alguna herramienta pueda hacer uso de la
base de datos, y buscar, descargar, e conf, e instalarlo.

cabal-get
---------
Es una herramienta para descargar e instalar paquetes cabal de hackageDB. Utiliza la interface XML-RPC.
Un usuario solo ejecuta: cabal-get install nombre_pkg
cabal-get resuelve las dependencias, descarga lo paquetes que faltan, los configura, construye en instala.
Es una herramienta muy similar a "agt-get"

Tambien existen otras herramientas que operan sobre Cabal: dh_haskell (para debian), cabal2rpm

Otras Herramientas
==================
+ make
+ hmake


Notas
=====
El Setup de Cabal fue inspirado por el Setup de Pyton (funcion defaultMain)

Objetivos de Cabal
==================
1.- [meta-data]
    Capturar informacion meta-data del paquete:
        * como construir
        * descripcion textual (humanamente leible) del paquete
        * Licencia
        ...
2.- [API]
    Especificar el CLI (Command-Line Interface)
        * como configurar
        * como construir
        * como instalar
3.- [Interface Library]
    Proveer una libreria para:
        * configurar
        * construir
        * instalar

Flujo de cabal:
    1.- El author crea un archivo que contiene la informacion meta-data del paquete
    2.- El autor distribuye el todo el paquete (fuente y meta-data)
    3.- El usuario final obtiene el paquete, y utiliza Cabal para construir e instalar
        el paquete.
