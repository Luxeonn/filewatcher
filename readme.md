# Runtime resource replacement

## Követelmények:
* IntelliJ IDEA
* exploeded deployment
* telepített war `web.xml`-ben a következő paraméterek:
    ```xml
    <context-param>
            <param-name>javax.faces.PROJECT_STAGE</param-name>
            <param-value>Development</param-value>
    </context-param>
    <context-param>
          <param-name>facelets.DEVELOPMENT</param-name>
          <param-value>true</param-value>
    </context-param>
    <context-param>
          <param-name>facelets.REFRESH_PERIOD</param-name>
          <param-value>1</param-value>
    </context-param>
    ```
* File Watcher plugin az IDEA-ban
* bash.exe a PATH környezeti változón 
 
## File Watcher beállításai:
#### Files to watch
* File type: figyelni kívánt fájl típus (pl.:`XHTML`, `JavaScript`, `CSS`)
* Scope: `web`
##### Scope létrehozása:
Azaz ahol figyeljen a plugin.
* Name: `web`
* Pattern: `file[<modul>]:src/main/webapp//*` (pl.: `file[bkv-frontend]:src/main/webapp//*`)
#### Tool to Run on Changes
* Program: [path\to\script\fileWatcherCopyFile.bat](scripts/fileWatcherCopyFile.bat) (pl.: `$ProjectFileDir$\bkv-wildfly-config\src\main\resources\file-watcher\fileWatcherCopyFile.bat`)
* Arguments: Programnak átadott paraméterek 
1. file:                   forrásfile elérési útja az aktuális könyvtárhoz viszonyítva
1. module:                 web modul neve, ahová a fájlt be kell mésolni
1. rootDirectoryForServer: gyökérkönyvtár, ahol lehet keresni a deployolt war állományt
1. logger:                 ha meg van adva, debug üzenet kiírása
    
    (pl.: `$FileRelativePath$ $ModuleName$ $ProjectFileDir$ xhtml_logger`)  		

* Working Directory and Environment Variables:
    * Working Directory: `$ProjectFileDir$\bkv-wildfly-config\src\main\resources\file-watcher`

### Vizuális segédlet:
File Watcher

![fw](img/File Watcher.JPG)

Scope

![fws](img/File Watcher scope.JPG)
 