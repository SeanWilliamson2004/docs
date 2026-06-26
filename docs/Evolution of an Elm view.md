---
title: Evolution of an Elm view
tags: []
description: 'This page is guidance on how to split out a child view from the parent
  view. Stick to the lowest stage possible. Stage 1: function Use this when : A…'
created: '2019-08-28'
modified: '2020-05-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Evolution%20of%20an%20Elm%20view.aspx
---

This page is guidance on how to split out a child view from the parent view. Stick to the lowest stage possible.

# Stage 1: function

Use this when :

- A child view is based around some entity or some related variables
- The child view is complicated enough that keeping it in the parent makes the code less readable

This is in `Main.elm`. A function can be written like so:


```
viewCar : String -> Int -> Html msg
viewCar make year = 
    ...

```
And called from your parent `view`. This is for views which do not need to send any messages back into your app.

# Stage 2: function with messages

Use this when

- The view needs to pass a message back into the app, maybe through an event like a button click or text input

Still in `Main.elm` If the view needs to show a button which adds a year to the car, and a text box which sets the car’s make. The messages may be:


```
    type Msg = AddYear | SetMake String

```
and the view:


```
viewCar : String -> Int -> Html Msg
viewCar make year = 
    ...
    , button [ onClick AddYear ]
    , input [ onInput SetMake ]

```
Notice that keeping `view` in `Main.elm` keeps things simple.

# Stage 3: Function placed in another module

Use this when

- `viewCar` is so complicated that it calls many other helper functions
- All of the helper functions are also complicated, and so can’t be defined in a small `let...in` clause in `viewCar`
- Those helper functions are only used for `viewCar`
- You want to hide those helper functions and only expose `viewCar`

**Remember**: Modules come with their own overhead, so it’s possible to overengineer and have too many modules. Use only if it’s worth hiding the helper functions.

When `viewCar` gets very complicated we can split it into another module. As `viewCar` is in another module, it shouldn’t know anything about your `Msg` Type. Therefore we need a generic type parameter, a lowercase `msg`. We need to pass into the view function the message for “add year” and “set the make”.


```
module Views.Car

viewCar :  msg -> (String -> msg) -> String -> Int -> Html msg
viewCar addYearMsg setMakeMsg make year = 
    ... -- calls many other helper functions in this module

```
## Optional stage: config

Use this when

- There are many parameters going into `makeCar`

At any stage (even stage 1\), if there are a lot of parameters passed into the view we can put them in a record and pass the record instead. Refactoring from stage 3 becomes:


```
type alias Config msg = 
    { addYear : msg
    , setMake : String -> msg
    , make : String
    , year : Int
    }
    
viewCar :  Config msg -> Html msg
viewCar config year = 
    ... 

```
# Stage 4: State

Use this when

- `makeCar` needs to store a variable which no other functions in `Main` need

`makeCar` may have a button which increases the text size. We need a variable `carTextSize : Int`. This variable can be held in the `Main` model, however no other view functions will need this variable, only `makeCar`. Therefore, it would be worth only exposing `carTextSize` to `makeCar` and hiding it from the rest of the app. We can do this by having an [opaque type](https://medium.com/%40ckoster22/advanced-types-in-elm-opaque-types-ec5ec3b84ed2) in the `View.Car` module called `State`:


```
module Views.Car exposing (Config, State, viewCar)

type alias Config msg = 
    { addYear : msg
    , setMake : String -> msg
    , make : String
    , year : Int
    , setState : State -> msg
    }
    
type State = State Int

initialState : State
initialState = State 1

viewCar :  Config msg -> State -> Html msg
viewCar config (State carTextSize) = 
    ... 
    button [ onClick (Config.setState (State (carTextSize + 1))) ] [ text "Increase text size"]

```
Notice that the module exposes `State` but not `State(..)`. So no other modules can construct a `State` or look into what data is within it. `Main.elm` will look like this:


```
import Views.Car as CarView

type alias model =
    { carViewState : CarView.State 
    ... --- other fields
    }

type Msg
    = SetCarViewState CarView.State
    | ... -- other messages
  
view model = 
    let
        carViewConfig = 
            { setState = SetCarViewState
            ... -- other config fields
            }
    in
    CarView.view carViewConfig model.carViewState

```
## Optional stage: state record

Use this when

- There is more than one variable in your `State`. This will be most of the time.

Lets say `viewCar` needs to also hold a `disabled` boolean. Everything stays the same in step 4, except our `State` looks a little different. In our `Views.Car` module:


```
type State = State State_

type alias State_ = 
    { carTextSize : Int
    , disabled : Bool
    }

initialState : State
initialState =
    State
        { carTextSize = 1
        , disabled = False
        }

viewCar :  Config msg -> State -> Html msg
viewCar config (State state) = 
    ... 

```
In Elm if we have an opaque type with a record, the convention is to give the record the same name as the opaque type but with an additional `_` suffix.

# Stage 5: A mini Elm app in your main Elm app

Use this when

- The view needs some state and also needs to emit some `Cmd`s
- You are in Stage 4, but there may be multiple Msgs emitted very quickly
- Each page in your application is so complicated that they could each be their own elm app

There is a *lot* of overhead with this approach so make sure you really need it and have ruled out all other designs. The idea is to have a module `Views.Car exposing (Model, init, Msg, update, view, subscriptions)`. This module is imported into your `Main` and you then use `Html.map`, `Cmd.map`, `Sub.map` and so on.

I have used this very rarely. One case is for login screens. My `Main.elm` is the login screen and my `App.elm` is the Elm app once we have logged in. The view function in `Main.elm` calls `App.view` if the `loggedIn` field in the `Model` is `True`. You can see an example of this in the PPS project, [here](https://codislimited.visualstudio.com/CodisDevelopment/_git/KewGreenDRPPP?path=/FrontEnd/elm/Main.elm&version=GC554be8a430396788d55b1e6a95e210cb2afa3b73).



# Stage 6: Shared state

Use this when:  


- You have multiple "mini elm apps" from stage 5, but all of them need to access and change some global variable.

Lets say you have multiple pages in your car application, each being a mini elm app. Any of the pages might make a call to the back end, and when we are waiting for the call to come back all pages must be disabled. In this case, you would need a disabled: Bool being given to all pages, and you would want any of the pages to be able to change this value.   
  
Solution: Create a new module:  
  
module GlobalState exposing (GlobalState, toggleDisabled)  
  
type GlobalState \= GlobalState GlobalState\_  
  
type alias GlobalState\_ \= { disabled : Bool }  
  
getDisabled : GlobalState \-\> Bool  
getDisabled (GlobalState state) \=  
    state.disabled  
  
toggleDisabled : GlobalState \-\> GlobalState  
toggleDisabled (GlobalState state) \=   
    GlobalState { state \| disabled \= not state.disabled }  
  
  
You don't expose the GlobalState constructors but you provide limited ways of editing the global state through functions like toggleDisabled, and ways of getting the values like getDisabled. You can hold more values in GlobalState and expose more edit/getter functions if need be. The GlobalState is held in the top level model.   
  
**Important**: Try to keep your GlobalState as small as possible, only hold variables here if necessary.  
  
Your page's init, view and update functions can now accept the GlobalState if they need it (if they don't need to access GlobalState, keep them as they are). The update function can also update the GlobalState if it wants:  
  
update : GlobalState \-\> Model \-\> Msg \-\> (Model, Cmd Msg, GlobalState)update globalState model msg \=     case msg of   
        SaveToBackEnd \-\> (model, httpCmd, GlobalState.toggleDisabled globalState)  
httpCmd : Cmd MsghttpCmd \= \-\- some cmd which makes a web request  
  
The parent model is responsible for holding the GlobalState, passing it around to pages and updating it if it gets a new GlobalState back from a page update function.
