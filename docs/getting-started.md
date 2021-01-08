# Getting Started

### Notice
This tutorial assumes you have experience creating mods for Minecraft 1.15; This includes writing mods entirely in Java, setting up the Forge MDK, adding new items/entites, etc. You won't be able to add vehicles using tools like MCreator.

## Create a New Project

To begin you will first need to create a new Forge modding environment. This tutorial is targetting Minecraft 1.15, so you'll want to download the corresponding [Forge MDK](https://files.minecraftforge.net/maven/net/minecraftforge/forge/index_1.15.2.html).  You'll want to do all the regular tasks such as loading the gradle project into your IDE, setting up version control, filling in `mods.toml` and `build.gradle`, and making sure your game loads.

## Adding the Dependencies

The next step is to add the Vehicle Mod into your modding environment. In order for you to add the Vehicle Mod though you will need to also add it's parent library Obfuscate. In order to do this we'll be using the [CurseMaven](https://github.com/Wyn-Price/CurseMaven) plugin by Wyn-Price. This plugin makes it easy to depend on [CurseForge](https://www.curseforge.com/minecraft/mc-mods) hosted mods.

In your `build.gradle` you'll need to add the following into your repositories.

```gradle
repositories{
	maven {
		url "https://www.cursemaven.com"
	}
}
```

Next in your dependencies it's simply a matter of adding the Obfuscate library and the Vehicle Mod. You'll want to use `fg.deobf` otherwise it won't work in a modding environment.

```gradle
dependencies {
	compile fg.deobf('curse.maven:obfuscate-289380:3148131') // 0.5.1
	compile fg.deobf('curse.maven:mrcrayfishsvehiclemod-286660:3103940') // 0.45.2
}
```

In your `mods.toml` you'll need to tell Forge that your mod depends on these mods to be present and loaded before yours.

```toml
[[dependencies.your_mod_id]]
    modId="obfuscate"
    mandatory=true
    versionRange="[0.4.3,)"
    ordering="AFTER"
    side="BOTH"
[[dependencies.your_mod_id]]
    modId="vehicle"
    mandatory=true
    versionRange="[0.44.0,)"
    ordering="AFTER"
    side="BOTH"
```

Now simply refresh gradle and the mods will be deobfuscated and added to the project. You should load up your game once and check the mod list to ensure they have been added. If you run into any problems where the files can't be found, make sure you are using at least Forge `1.15.2-31.2.0` and CurseMaven `2.1.4`

![Mod List](img/mod_list.png)

## You're Ready

Congratulations, you're now ready to start creating a Vehicle Mod addon! You can now move onto [creating your first vehicle](/first-vehicle).

Before continuing, consider making your addon open source. Eventually a list of addons will be formed and allowing other developers read your code helps them develop their own addon.
