# NoesisGUI Unreal Engine 4.18 Plugin

## Introduction

This document will guide you through the process of setting up the NoesisGUI Unreal Engine plugin, and how to get started using NoesisGUI in your Unreal Engine project.

NoesisGUI is a hardware accelerated, vector graphics User Interface solution based on XAML.

Some knowledge of both Unreal Engine as well as the NoesisGUI SDK is assumed, but this document attempts to be as thorough as possible.

## Requirements

In order to use NoesisGUI in your UE4 project, you're going to need:

* Unreal Engine, with source code. This can be either a pre-built version installed through the Epic Games Launcher, or a version built by yourself from the source in GitHub. To install a pre-built version of Unreal Engine, please refer to the document [Installing Unreal Engine](https://docs.unrealengine.com/latest/INT/GettingStarted/Installation/index.html) and follow the instructions there. For instructions on how to get a copy of the Unreal Engine source code and how to build it, please refer to the README.md document on their [GitHub repository](https://github.com/EpicGames/UnrealEngine).

* This Unreal Engine plugin.

* The NoesisGUI SDK version 2.1. You can download it from [our website](https://noesisengine.com).

## Samples

After you read this document, we have a few samples so you can see some of the concepts in action:

* [Buttons](https://github.com/Noesis/Tutorials/tree/master/Samples/Buttons/UE4): A simple game that shows how you can use `Binding`s to implement `Command`s as `Blueprint` functions.

* [Widget3D](https://github.com/Noesis/Tutorials/tree/master/Samples/Widget3D/UE4): A similar UI, but this time presented in 3D using Unreal Engine's `WidgetComponent`.

* [Login](https://github.com/Noesis/Tutorials/tree/master/Samples/Login/UE4): A slightly more elaborated sample that uses `Binding`s to data and functions in a `Blueprint`, combined with some C++ code for more advanced functions.

* [QuestLog](https://github.com/Noesis/Tutorials/tree/master/Samples/QuestLog/UE4): This samples shows how to use `Binding`s to more complex data, such as `Texture`s and `Array`s of `Object`s.

* [Scoreboard](https://github.com/Noesis/Tutorials/tree/master/Samples/Scoreboard/UE4): This sample shows more advanced ways to expose data on `Blueprint`s so that it can be used in `Binding`s, such as using Getter functions and manually notifying property changes.

* [Menu3D](https://github.com/Noesis/Tutorials/tree/master/Samples/Menu3D/UE4): This sample shows how to use `UseControl`s to implement a multi-panel game main menu.

* [ShooterGame](https://github.com/Noesis/UE4-ShooterGame): This sample replaces the UI from Epic's ShooterGame sample with NoesisGUI. Some changes were dome to the source code in order to expose data and functionality, but otherwise the UI is done completely in `Blueprint`.

## Setup

The setup process is slightly different depending on whther you're using a version of Unreal Engine installed trough the Epic Games Launcher or built by yourself from the source code in GitHub.

You can use the NoesisGUI Unreal Engine plugin as either an Engine plugin or a Project (Game) plugin. For more information about Unreal Engine Plugins, please refer to the [Plugins](https://docs.unrealengine.com/latest/INT/Programming/Plugins/index.html) documentation.

### Setup with Epic Games Launcher version

1. Make sure you have the engine source code installed. To verify you do, go to the Unreal Engine tab in the Epic Games Launcher, then go to your library of installed components. From there, at the top, look for the Unreal Engine version with which you wish to use NoesisGUI, and from the drop down list next to the Launch button, selecto options. Make sure the Engine Source option is selected. If it isn't, click on the tick box next to it and then click Apply to download it.

![Installed Engine version options](https://noesis.github.io/NoesisGUI/UE4Plugin/VersionOptions.png)
![Engine Source installed](https://noesis.github.io/NoesisGUI/UE4Plugin/EngineSource.png)

2. Copy the contents of this repository into `[UE4Root]/Engine/Plugins/NoesisGUI` if you want to use it as an Engine plugin, or `[ProjectRoot]/Plugins/NoesisGUI` if you choose to use it as a Project plugin. We'll refer to the directory where you install the plugin as `[NoesisGUIPlugin]` from now on. The plugin assumes it will be installed on either of these paths, and will crash on load if it isn't. For example, don't copy it into a sub-directory such as `[UE4Root]/Engine/Plugins/UI/NoesisGUI`.

3. Download the NoesisGUI SDK version 2.1 from [our developer portal](http://noesisengine.com/forums/) and extract it into `[NoesisGUIPlugin]/Source/Noesis/NoesisSDK`.

4. If you've installed the plugin as an Engine plugin you need to run `[NoesisGUIPlugin]/BuildNoesisGUIPlugin.bat` to finish the setup. This step is not required if you've installed it as a Project plugin.

### Setup with source code from GitHub

1. Download or clone the Unreal Engine source code from GitHub. You can find more information about how to do this in the document [Downloading Unreal Engine Source Code](https://docs.unrealengine.com/latest/INT/GettingStarted/DownloadingUnrealEngine/index.html).

2. Copy the contents of this repository into `[UE4Root]/Engine/Plugins/NoesisGUI` if you want to use it as an Engine plugin, or `[ProjectRoot]/Plugins/NoesisGUI` if you choose to use it as a Project plugin. We'll refer to the directory where you install the plugin as `[NoesisGUIPlugin]` from now on. The plugin assumes it will be installed on either of these paths, and will crash on load if it isn't. For example, don't copy it into a sub-directory such as `[UE4Root]/Engine/Plugins/UI/NoesisGUI`.

3. Download the NoesisGUI SDK version 2.1 from [our developer portal](http://noesisengine.com/forums/) and extract it into `[NoesisGUIPlugin]/Source/Noesis/NoesisSDK`.

4. Regenerate the Unreal Engine project files. You can do this in a number of ways, some of which are explained in the [Automatic Project File Generation](https://docs.unrealengine.com/latest/INT/Programming/UnrealBuildSystem/ProjectFileGenerator/index.html) document.

5. Build the Engine or your Project. The NoesisGUI plugin should be built along with it.

## Directory structure

If all the steps so far have been successful, your Unreal Engine install should contain the following directories. Please note that only the directories relevant to the NoesisGUI plugin are listed here, and that your installation may contain additional files and directories that have been omitted here for clarity.

```
[NoesisGUIPlugin]
+-- Binaries
+-- Content
+-- Intermediate
+-- Resources
+-- Shaders
+-- Source
    +-- Noesis
        +-- NoesisSDK
            +-- Bin
            +-- Include
            +-- Lib
            +-- version.txt
    +-- NoesisEditor
    +-- NoesisRuntime
+-- NoesisGUI.uplugin
```

## Enabling and configuring the plugin

At this point the plugin should be ready to use, so we can proceed to enable it and configure some settings for your project.

1. Run the Unreal Engine editor. You may get an alert on the bottom right corner alerting you that new plugins have been installed. If you don't, open the Plugins dialog from the Edit menu, and selecting UI from the category list on the left. You can enable the plugin from the right hand panel.

![Ensuring the NoesisGUI plugin is enabled](https://noesis.github.io/NoesisGUI/UE4Plugin/Plugins.PNG)

You can also do this manually by modifying your Project's `.uproject` file to add the plugin dependency, like this:

```
"Plugins": [
    {
        "Name": "NoesisGUI",
        "Enabled": true
    }
]
```

2. With the plugin enabled, you can configure some NoesisGUI global settings for your project. You can find them by opening the Project Settings dialog from the Edit menu, then scrolling down to the Plugins section on the left panel, and finally NoesisGUI. These settings have sensible default values, so if you're unsure about them you can just leave them as they are. If you modify these settings you will have to restart the editor for the changes to take effect.

![NoesisGUI plugin settings](https://noesis.github.io/NoesisGUI/UE4Plugin/NoesisPluginSettings.PNG)

## Setting up your Unreal Engine project to use NoesisGUI

The process to set up you project to work with NoesisGUI depends on whether it is a Blueprint Only project or a C++ project.

For a Blueprint Only project, enabling the plugin as described above is all you need to do.

For a C++ project, there are two additional steps. First, you must add the module dependencies to your project. To do that, simply add the following line to you module's ModuleRules derived class (in your module's .Build.cs file):

```
PrivateDependencyModuleNames.AddRange(new string[] { "Noesis", "NoesisRuntime" });
```

Next, you have to `#include` the necessary headers for your project. To simplify this we've created a single header file you can include, preferably in your game project's PCH file. Just add the following line:

```
#include "NoesisRuntime.h"
```

## Using NoesisGUI with Unreal Engine

With the NoesisGUI plugin for Unreal Engine you have all the power of the native NoesisGUI SDK at your disposal. There are a few particularities about the use that will be explained later, but the bottom line is that everything that can be done with the native SDK will work in Unreal Engine.

But we wanted to provide an easy way to allow users to leverage the power of NoesisGUI using Unreal Engine's `Blueprint`s. A mechanism is provided that allows `Binding`s to `Blueprint` properties, without having to write a signle line of C++ code.

With this approach NoesisGUI will be more accesible for everyone, but at the same time will allow more advanced users to use the native SDK directly, with the complete set of features available to them as in any other platform.

## Importing your assets

At this point you're ready to start using NoesisGUI in your project. The first step is importing your assets. These will consist of XAML files, fonts and images. The best way to work with NoesisGUI assets in Unreal Engine is to put them in your game's Content folder. They will be automatically imported into Unreal Engine, and any modifications you make will be automatically re-imported. After import, your XAML files will appear in Unreal Engine's Content Browser as `NoesisXaml` assets, while your images will appear as `Texture2D`s and fonts will appear as `Font`s and `FontFace`s.

![Imported assets](https://noesis.github.io/NoesisGUI/UE4Plugin/Assets.PNG)

### Absolute URIs and Unreal Engine

When importing your XAML files, these may contain references to other XAML files, as well as images and fonts, as stated above. These references may be in the form of relative or absolut URIs. When working with absolute URIs in Unreal Engine, these are considered as relative to the Content folder of your game project.

Please refer to the document [URIs in NoesisGUI](https://www.noesisengine.com/docs/Gui.Core.URIs.html) for more information.

## Creating a View for your XAML

Now that we have our assets imported into the game, we have to create a View for it. We do this from the Content Browser, by using either the Add New button or by right clicking on the Content Browser itself. Then choose NoesisGUI and Noesis View.

![Adding a new Noesis View](https://noesis.github.io/NoesisGUI/UE4Plugin/NoesisView.PNG)

After naming the newly created asset, open it. You will be presented with the familiar Blueprint Class editor. Click on the Class Settings button at the top, where you will find the NoesisGUI properties.

![Class Settings button](https://noesis.github.io/NoesisGUI/UE4Plugin/ClassSettings.PNG)

The most important of all is the XAML property. Here you'll reference the NoesisXaml for which you want to create hte View. Enable PPAA allows you to enable per-primitive antialiasing, in case you're not using multisampling on your main render target. Tessellation Quality lets you select the degree of subdivision for your path geometry.

![Noesis View settings](https://noesis.github.io/NoesisGUI/UE4Plugin/NoesisViewSettings.PNG)

After compiling and saving your NoesisView, we are ready to use it.

## Using a NoesisView

A NoesisView is also an Unreal Engine UMG Widget. This means that you can use it wherever a native UMG Widget is used, so if you're familiar with Unreal Engine's UMG system it will be very simple to get up and running with NoesisGUI. Please, refer to the document [Creating Widgets](https://docs.unrealengine.com/latest/INT/Engine/UMG/UserGuide/CreatingWidgets/index.html) for information about how to add a NoesisView to your viewport and how to handle input. Because a NoesisView is also an UMG Widget it means you can also create 3D UI elements by using a Widget Component. Please, refer to the document [Widget Components](https://docs.unrealengine.com/latest/INT/Engine/Components/Widget/) for more information.

![Creating a Widget from a NoesisView and adding it to the viewport](https://noesis.github.io/NoesisGUI/UE4Plugin/CreateWidget.PNG)

## NoesisGUI Property Binding in Unreal Engine

One of the most powerful features of NoesisGUI is the support for a Model-View-ViewModel pattern through [Data Binding](https://www.noesisengine.com/docs/Gui.Core.DataBindingTutorial.html) This is made even more powerful in Unreal Engine by combining it with the graphical scripting capabilities provided by Blueprints.

When you create a NoesisView for a NoesisXaml and you create a Widget from it, the instantiated object itself is set as the Data Context. You can also override this behaviour by calling the function Set Data Context on the NoesisView itself and specifying a different Unreal Engine Object.

Whether you decide to use the NoesisView or any other Object as the Data Context, you can define in in properties that can be bound to your XAML, as described in the aforementioned document. You can define a property in two ways:

* As a variable. The name of the property for binding purposes will be the name of the variable.

![Multiple Properties implemented as Blueprint variables](https://noesis.github.io/NoesisGUI/UE4Plugin/VariableProperties.PNG)

* As a Get<PropertyName> function that has no input parameters and a single output parameter, with alternatively a Set<PropertyName> function with no output parameters and a single input parameter of the same type as the output parameter of the Get function. The name of the property for binding purposes will be <PropertyName>.

![InfiniteAmmo Property implemented as a pair of Get/Set functions](https://noesis.github.io/NoesisGUI/UE4Plugin/FunctionProperty.PNG)

Here's a table with the types supported for Data Binding and the corresponding native NoesisGUI SDK types. Whenever there was a native Unreal Engine type that could work we've decided to use that instead of creating a new type.

Unreal Engine Type | NoesisGUI Type
-------------------|--------------------------
Boolean|bool
Integer|int32_t
Float|float
String|NsString
Color|Noesis::Color
Vector2D|Noesis::Point
NoesisRect|Noesis::Rect
NoesisSize|Noesis::Size
NoesisThickness|Noesis::Thickness
NoesisCornerRadius|Noesis::CornerRadius
NoesisTimeSpan|Noesis::TimeSpan
NoesisDuration|Noesis::Duration
NoesisKeyTime|Noesis::KeyTime
Texture2D|Noesis::ImageSource
TextureRenderTarget2D|Noesis::ImageSource

The plugin also supports custom Blueprint Enums, Structures and Classes. Blueprint Structures and Classes work similarly and they both expose their members as subproperties. The difference is that Structures are treated as atomic objects, and the performance characteristics are different. We recommend you use Blueprint Classes for long lived objects, and Blueprint Structures for small objects with shorter lifespans that don't require a full Blueprint Class.

We also support Arrays of the aforementioned types, which are exposed as a List to the Binding system.

Additionally we support binding of Blueprint functions to NoesisGUI Commands. A function that either takes no parameters, or takes a parameter of type Object, and has no output function will be turned into a functor implementing the Noesis::ICommand interface. If you also add a function with the same name but prefixed with CanExecute that takes no parameters and returns a Boolean, it will be used to decide whether the command can be executed.

![JoinGame Command with CanExecute companion function](https://noesis.github.io/NoesisGUI/UE4Plugin/Command.PNG)

## Property Binding and notifications

Performance is a key concern of NoesisGUI. For this reason, instead of polling all the data sources for all bound properties in every update, it uses a reactive model in which the user notifies NoesisGUI that a property has changed and the system updates the minimum possible set of its internal structures affected by that change.

In the NoesisGUI Native SDK this is achieved by having your classes implement the Noesis::INotifyPropertyChanged or Noesis::INotifyCollectionChanged interfaces. The typical implementation exposes Set functions that compare the new value with the old and notify any potential listeners if they are different.

To simplify this in Unreal Engine, we've provided custom nodes that you can use in your Blueprint code that replace the standard Set Property and array operations with custom versions that, additionally notify listeners if necessary. Here's a table with the native Unreal Engine nodes and the corresponding NoesisGUI ones:

Unreal Engine Node | NoesisGUI Node
-------------------|---------------
Set|Set w/ NotifyChanged
Add (Array)|Add w/ NotifyArrayChanged
Add Unique (Array)|Add Unique w/ NotifyArrayChanged
Shuffle (Array)|Shuffle w/ NotifyArrayChanged
Append Array (Array)|Append Array w/ NotifyArrayChanged
Insert (Array)|Insert w/ NotifyArrayChanged
Remove Index (Array)|Remove Index w/ NotifyArrayChanged
Remove Item (Array)|Remove Item w/ NotifyArrayChanged
Clear (Array)|Clear w/ NotifyArrayChanged
Resize (Array)|Resize w/ NotifyArrayChanged
Set Array Elem (Array)|Set Array Elem w/ NotifyArrayChanged

![Automatic notifications using our custom nodes](https://noesis.github.io/NoesisGUI/UE4Plugin/AutomaticNotification.PNG)

Using this function is the most convenient way to notify NoesisGUI of changes in your data. But sometimes it is necessary to manually notify that a property has changed. This is the case, for example, when a property is implemented as a pair of Get/Set functions, that are not bound to a variable and therefore don't allow you to use these nodes. For these situations you can manually call the functions NotifyChanged and NotifyArrayChanged, passing the name of the property.

![Manual notification of a Property implemented as a pair of Get/Set functions](https://noesis.github.io/NoesisGUI/UE4Plugin/ManualNotification.PNG)

## Logging and debugging

If following the previous steps you still can't see your NoesisGUI interface, the first step would be to take a look at the Output Log window. You can select the verbosity of the output from the plugin settings, as described above. The default setting is Quiet, and won't output anything. Normal will allow you to discover common errors, and Binding also provides extra information about the Binding system which is separated form the rest as it can be quite detailed.

Additionally logging messages in NoesisGUI have several levels of verbosity. Here is a table with the levels defined by NoesisGUI and how they map to Unreal Engine:

NoesisGUI Verbosity Level | Unreal Engine Verbosity
--------------------------|------------------------
Trace|VeryVerbose
Debug|Verbose
Info|Log
Warning|Warning
Error|Error

You can filter the NoesisGUI log messages by selecting the LogNoesis  category from the Categories drop down list.

![Unreal Engine Output Log categories](https://noesis.github.io/NoesisGUI/UE4Plugin/OutputLogCategories.PNG)

## Known Issues

There are a couple of issues of which we are aware of and are either out of our control or we are working to resolve.

* NoesisViews don't compile correctly if the Blueprint Compilation Manager is enabled. The feature seems to disable the custom Blueprint compiler for NoesisViews, which results in unusable widgets. We are investigating the problem and will get in touch with Epic about it. For now, please disable the Blueprint Compilation Manager by opening the Project Settings dialog from the Edit menu, then scrolling down to the Editor section on the left panel, and finally Blueprints and uncheck the Use Compilation Manager on the right panel.

![Disabling Blueprint Compilation Manager](https://noesis.github.io/NoesisGUI/UE4Plugin/BlueprintCompilationManager.PNG)

* It is not possible to change the cursor to use with a NoesisView generated Widget by using the Set Cursor function. This will be fixed in a future release.

![Set Cursor does not work at the moment](https://noesis.github.io/NoesisGUI/UE4Plugin/SetCursor.PNG)

## Troubleshooting

* When you try to build, package or launch your project you get an error complaining about missing libraries `UE4-NoesisRuntime.lib` or `UE4-NoesisRuntime-Win64-Shipping.lib` (`UE4-NoesisRuntime.a` or `UE4-NoesisRuntime-Mac-Shipping.a` on Mac).

    * If you're using an Epic Games Launcher version of Unreal Engine and you decided to install the plugin as an Engine plugin, please run the `BuildNoesisGUIPlugin.bat` (`BuildNoesisGUIPlugin.command` on Mac) to build the runtime libraries needed.

* When starting your project editor you get an error because your game module could not be loaded.

    * Make sure you enabled the plugin for your project before adding the dependency to the module `NoesisRuntime`. If you already had a project created, simply add the dependency manually as described in the section [Enabling and configuring the plugin](#enabling-and-configuring-the-plugin).

* In windows, if you get a crash on startup with `__delayLoadHelper2` on the top, that means `NoesisRuntime` cannot find `Noesis.dll`.
    
    * Make sure the plugin is located in `[UERoot]/Engine/Plugins/NoesisGUI` or `[ProjectRoot]/Plugins/NoesisGUI`, and not in any subfolders, as explained in the [Setup with Epic Games Launcher version](#setup-with-epic-games-launcher-version) and [Setup with source code from GitHub](#setup-with-source-code-from-github) sections.