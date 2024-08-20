# Community Language Repositories

Localisation for GameMaker is pulled from the repositories listed below. Each repository contains the localised strings for a particular language:

* [French](https://github.com/YoYoGames/IDE_Localisation_French)
* [Italian](https://github.com/YoYoGames/IDE_Localisation_Italian)
* [Japanese](https://github.com/YoYoGames/IDE_Localisation_Japanese)
* [Korean](https://github.com/YoYoGames/IDE_Localisation_Korean)
* [Polish](https://github.com/YoYoGames/IDE_Localisation_Polish)
* [Russian](https://github.com/YoYoGames/IDE_Localisation_Russian)
* [Portuguese (Brazilian)](https://github.com/YoYoGames/IDE_Localisation_PortugueseBrazilian)
* [German](https://github.com/YoYoGames/IDE_Localisation_German)
* [Spanish](https://github.com/YoYoGames/IDE_Localisation_Spanish)
* [Chinese](https://github.com/YoYoGames/IDE_Localisation_Chinese)

Each repository contains a **[language].csv** file with general strings for the IDE, and a **[language]_dnd.csv** file with strings used in GML Visual.

You can contribute to these files by simply forking the repository, making your changes and making a PR to merge your forked changes into the original repository.

# Plugin Loading

The GameMaker Package Manager (currently in 2024.800+ betas only) can be used to load a language plugin manually.

Open **Tools** -> **Package Manager** and click on the (+) button in the top right.

Click on (+) again below the list that shows GMRT. This will open a dialog where you can add the Localisation Plugins source:

![image](https://github.com/user-attachments/assets/be18680d-49b1-4807-b71b-a557bf7a603f)

```
Name: Localisation Plugins
URL: https://gmpm.gamemaker.io/
Scopes: @localisation_plugins
Install Subdirectory: LocalisationPlugins
```

Now all languages will appear in the Package Manager when this new source is selected:

![image](https://github.com/user-attachments/assets/5fa8de50-9bcb-4780-a48e-b9458dec99d2)

