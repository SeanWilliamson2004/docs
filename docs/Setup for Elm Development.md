---
title: Setup for Elm Development
tags: []
description: Setup Elm Install Elm from the website. At the time of writing, the current
  version is 0.19.1. Make sure it's added to PATH. Install VSCode Install…
created: '2020-05-15'
modified: '2020-05-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Curriculum%20for%20Elm%20Development.aspx
---

# Setup Elm

1. Install Elm from the website. At the time of writing, the current version is 0\.19\.1\. Make sure it's added to PATH.
2. Install VSCode
3. Install an extension for Elm development. At the time of writing, [this is the best one](https://marketplace.visualstudio.com/items?itemName=Elmtooling.elm-ls-vscode). Make sure you follow the installation instructions.
4. In the VSCode settings, turn FormatOnSave to True. If auto formatting doesn't work you may need to increase the format on save timeout settings.
5. Test it out by creating a new directory, running elm init inside it using powershell, then under the src folder add a Main.elm and paste in any small one\-page elm program, these can be found on the [guide](https://guide.elm-lang.org/).

You should get auto complete, code hints etc. If you press Enter a few times in the middle of the code to create extra new lines, you should see those new lines dissapear when you save.  
  
# Codis curriculum

## Beginning

1. Learn how to use the navigation features of VSCode. Elm files are longer than other languages like VB.net. In VB.net, if a file is long, it suggests that a class is too big which is usually a design problem. This isn't the case with an Elm module. It makes elm development a lot easier when you are less reliant on scrolling to find what you want, and more reliant on things like the breadcrumb, outline view, go to symbol, find all references, to to definition (ctrl\-click) etc. Google these terms for more help with VS Code. **If you find yourself scrolling a lot when writing elm, actively stop yourself to get out of the habit**.
2. Make your way through the [elm guide](https://guide.elm-lang.org/). It's important that you are comfortable with every topic here, however you **don't** need to read about Navigation, Url Parsing, Optimization and the appendicies.
3. Don't just read the guide, try to make your own sample applications which aren't the same as the ones in the guide but use the concepts.
4. Go through the [excercises here](https://github.com/robertjlooby/elm-koans) (read the readme for instructions, run the app in your browser using "elm live" (see the readme) and keep the browser open as you edit the elm files).
5. Important APIs to know off by heart and use in your application:
1. Forward pipe \|\> , backward pipe \<\| , forward composition \>\> , backward composition \<\<
2. List. map, filter, interpsere, sortBy, length, concat. (Go through and understand all the list APIs, but these you should know off by heart)
3. Maybe. map, andThen, withDefault
4. Result. map, andThen, withDefaut, toMaybe
5. Task. map, andThen, perform
6. Cmd.map
7. Sub.map
8. Html.map (notice a pattern with map and andThen?)

7. Understand [opaque types](https://medium.com/%40ckoster22/advanced-types-in-elm-opaque-types-ec5ec3b84ed2) and [extensible records](https://medium.com/%40ckoster22/advanced-types-in-elm-extensible-records-67e9d804030d).

## Intermediate

1. [Clone this repository](https://codislimited.visualstudio.com/TestProject/_git/Elm.Exercises), read the ReadMe and go through the exercises.
2. Watch these and try to write some sample code which uses the concepts in these videos:
1. [Make Data Structures](https://www.youtube.com/watch?v=x1FU3e0sT1I)
2. [The life of a file](https://www.youtube.com/watch?v=XpDsk374LDE)
3. [Scaling elm apps](https://www.youtube.com/watch?v=DoA4Txr4GUs)
4. [Immutable relational data](https://www.youtube.com/watch?v=28OdemxhfbU)

4. Write an application which has a form (eg first name, last name, age). Now refactor this application to go through each stage of the [evolution of an elm view](Evolution of an Elm view.md). **Note**: In real life you would stick to the smallest, simplest stage until you had to go up a stage, but go through each stage with a simple form for the sake of excercise.
5. Use some [CodisViews](https://codislimited.visualstudio.com/CodisDevelopment/_git/Elm.Views?path=/README.md&_a=preview) components in a project, the ReadMe will show you how to install into your project. Look at the [Demo project](https://codislimited.visualstudio.com/CodisDevelopment/_git/Elm.Views.Demo?path=/README.md&_a=preview) to see how each of the components are used. The [PPS project](https://codislimited.visualstudio.com/CodisDevelopment/_git/KewGreenDRPPP?path=/README.md&version=GBmaster&_a=preview) is another example of how CodisViews are used. Try adding:
1. A DatePicker
2. Animated Logo
3. Dialog box
4. Table

7. Understand the architecture used in PPS, as this is common to most Elm apps. Main is the login screen where all the pre\-requisites are loaded (such as css files, etc). The user logs in, Main.elm logs in and retrieves some large list of entities, which should be familiar to you from the "immutable relational data" video above. Every web request to the back end which amends these entities (eg "Add Group"), the web request performs the update and then returns a brand new updated list of entities.
