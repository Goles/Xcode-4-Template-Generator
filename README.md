# Xcode 4 Template Generator

Based on the original code by __Ricardo Quesada__ for the cocos2d project, modifications & ugly hacks by [Nicolas Goles Domic](http://www.twitter.com/ngoles/)

## Info

The Xcode 4 template generator, is a simple script written in Python to aid in the rather obscure process of creating Xcode 4 templates. As you may already be aware, Xcode 4 templates are very different from Xcode 3 templates, so taking a look at Boreal's Kiss "A minimal project template for Xcode 4" is recommended. In that article you will find a lot of information about what is currently known about the new Template System.

[A minimal project template for Xcode 4](http://blog.boreal-kiss.net/2011/03/11/a-minimal-project-template-for-xcode-4/)

## Usage

This script was created with the goal of make it usable by continuous integration (C.I) tools or "meta template building scripts" in order to keep some library templates updated, but can also be used as a stand alone tool.

Let's say you want to manually create an iOS _Window-based Application_ template that includes the Box2d library:

1. Put the **Box2d** folder in the same directory as _template_generator.py_
2. Execute: `python template_generator.py --concrete no --directory Box2d --description "box2d library template" --identifier com.yoursite.box2dlib` (This should create a **Box2d.xctemplate** folder, which should contain the **Box2d** folder and a _TemplateInfo.plist_ file)
3. Execute: `cp -R /Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/Project\ Templates/Application/Window-based\ Application.xctemplate .`
4. Open the _TemplateInfo.plist_ inside the "**Window-based Application.xctemplate**" folder with your Text Editor of choice or _.plist_ editor and add a new ancestor (`line 5`) referencing _com.yoursite.box2dlib_ (matches identifier of step 2), also change the identifier to _com.yoursite.modified_window_application_ (around `line 21`).
5. Make a new folder named **Window_Based_App_plus_Box2d** and move both the **Box2d.xctemplate** and "**Window-Based Application.xctemplate"** folders into it.
6. Copy the **Window_Based_App_plus_Box2d** folder into `~/Library/Developer/Xcode/Templates`

You should be able to create a new Xcode 4 project using this template now.

**Note**: To learn out what the keywords _concrete_, _description_ and _identifier_ mean, checkout the link provided in the usage section of the wiki.

**Note 2**: If you run ./template_generator.py without a directory arg, it will print a help screen with information about each possible flag.

## To-Do

* Pass "project settings" as parameters, so that for example we can specify header search paths to our templates.
* Clean the code, this is my first python script, so I'm sorry if it's not neat :)
* Add new cool features.

## Important

Creating invalid Xcode 4 templates can be dangerous as described in the link provided in the **info** section, please read about it and be careful.
