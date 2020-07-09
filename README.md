# sts_modding_tutorial
Getting into STS modding

## Make a dedicated modding dev folder (assume we have ~/modding)
  - Make a ~/modding/lib folder
  - Copy desktop-1.0.jar from the SlayTheSpire directory here
  - Copy ModTheSpire.jar and BaseMod.jar here as well

## Make a new project 
  - Select Maven from the list on the left
  - Put it in the proper place (if ~/modding/lib exists, this should go in ~/modding)
  - Give it whatever name
  - Make sure to select the Java 1.8 SDK

## Open up the pom.xml file in the editor
  - Remove everything in there and replace with the following default stuff
  - https://gist.githubusercontent.com/alexdriedger/fb74397086ee80073417f19d6305bb05/raw/5ad46ff357169a106f9464b574134d718d257442/pom.xml
  - Change all the placeholder ExampleMod text with the name of your mod (should be relatively intuitive what needs changing if you go line by line)

## Alter the project structure to include the dependencies correctly
  - File->Project Structure (or Control+Alt+Shift+S)
  - Navigate to the "Modules" subwindow
  - In my setup, the "Export" area only contains "1.8 Java" and "<Module Source>" -- we're missing the required dependencies from this list by default
      * We need to do the following steps for each .jar lib file we need to import
      * These are: desktop-1.0.jar, ModTheSpire.jar, and BaseMod.jar
      * Click the "+" icon to the right of the Export list (choose "JARs or Directories")
      * Navigate to the ~/modding/lib folder we made and click on the .jar file and hit OK
      * Each time we do this, the proper import should show up in our Export list
      * Repeat for the remaining dependencies
  - Now, our "Export" list area should contain:
      * 1.8 (Java)
      * " < Module source >"
      * desktop-1.0.jar
      * ModTheSpire.jar
      * BaseMod.jar
  - Make sure the checkbox next to each of our depencies is checked (it isn't by default)
  - Hit OK to leave our project structure screen

## Add information for ModTheSpire to identify our mod
  - Create a new file in the src/main/resources folder
  - Call it "ModTheSpire.json"
  - Add the following in here and then tweak as needed:
```json 
{
  "modid": "example",
  "name": "Example Mod",
  "author_list": ["kiooeht"],
  "description": "An example mod to be an example.",
  "version": "0.1",
  "sts_version": "03-29-2018",
  "mts_version": "2.6.0",
  "dependencies": ["basemod"]
}
```

## Building a JAR file using Maven
  - View->Tool Windows->Maven
  - Expand your mod, then "Lifecycle"
  - Right click "package" -> "Run Maven Build"
  - If all goes right, you should see a build success in the output window
  - TIP: I like to make a shorcut to this build option since it's used a lot
    * File->Settings->Keymap
    * Search for "Maven" in the search box top right
    * Look for our package build option we just did, then right click it and add a shortcut
    * I use Ctrl+R for mine and it works pretty well
