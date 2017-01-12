# The Official Grassdancer C# Style Guide

## Inspiration

This style guide outlines the basic stylistic rules to follow when writing code for Grassdancer. The document you're reading is originally forked from the [raywenderlich](https://github.com/raywenderlich/c-sharp-style-guide/blob/master/README.markdown) style guide, and significantly altered based on our team's own style decisions.

The goals of this style guide are **conciseness**, **readability**, and **ease of use** for the entire Sugarscape team.

## Table of Contents

- [Visual Studio Settings](#visual-studio-settings)
- [Nomenclature](#nomenclature)
  + [Script Files](#script-files)
  + [Classes & Interfaces](#classes--interfaces)
  + [Services](#services)
  + [Functions](#Functions)
  + [Fields](#fields)
  + [Parameters](#parameters)
  + [Delegates](#delegates)
  + [Events](#events)
  + [Coroutines](#coroutines)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
  + [Enums](#Enums)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Commenting](#commenting)
  + [Classes and Functions](#classes-functions)
- [Unity Editor](#unity-editor)
  + [Exposed Variables](#exposed-variables)
- [GameManager and Services](#gamemanager-services)
  + [Accessing a Service](#accessing-a-service)
- [Credits](#credits)


## Visual Studio Settings
[Here](https://drive.google.com/open?id=0Bxad50Rx4CmIbXZjQmdtOFVlNE0) is a policy file that can be imported into Visual Studio to set up automatic formatting. 

It can be imported through Tools->Import and Export Settings->Import selected environment settings. Click on the settings file and you should be good to go. 

*This will not overwrite your syntax highlight settings and color scheme*
## Nomenclature

On the whole, naming should follow C# standards.

### Script Files

Script files are all __UpperCamelCase__, multiple words concatenated together,
without
hyphens or underscores:

__BAD__:

```c#
game_Manager.cs
```

__GOOD__:

```c#
GameManager.cs
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example, `RadialSlider` 

DO add the suffix __Service__ to all Interfaces used for Services.

__BAD__:

```c#
Interface IAudioServiceInterface
```

__GOOD__:

```c#
Interface IAudioService
```

### Services

DO add the suffix __Manager__ to names of Services

__BAD:__

```c#
public class AudioService: MonoBehaviour, IAudioService
```
__GOOD:__

```c#
public class AudioManager: MonoBehaviour, IAudioService
```

### Functions

Public functions are written in __UpperCamelCase__. For example, `DoSomething`

Private functions are written in __lowerCamelCase__. For example, `doSomething`

__BAD__:

```c#
private void MyFunction()
```

__GOOD__:

```c#
private void myFunction()
```

### Fields

Written in __lowerCamelCase__.

Static fields, including singletons, should be written in __UpperCamelCase__:

```c#
public static int TheAnswer = 42;
```

All non-static fields are written __lowerCamelCase__. Per Unity convention, this includes __public fields__ as well.

For example:

```C#
public class MyClass {
  public int publicField;
  int packagePrivate;
  private int myPrivate;
  protected int myProtected;
}
```

Private non-static fields should start with a lowercase letter.

__BAD:__

```c#
private int _myPrivateVariable
```

__GOOD:__

```c#
private int myPrivateVariable
```

Local versions of UnityEngine reserved names should be named mComponentName unless a more specific name is desired.

__BAD:__

```c#
private Rigidbody rigidbody;
```

__GOOD:__

```c#
private Rigidbody mRigidbody;
```

### Parameters

Parameters are written in __lowerCamelCase__.

__BAD:__

```c#
void doSomething(Vector3 Location)
```
__GOOD:__

```c#
void doSomething(Vector3 location)
```

Single character values to be avoided except for temporary looping variables.

### Delegates

Delegates are written in __UpperCamelCase__.

When declaring delegates, DO add the suffix __EventHandler__ to names of delegates that are used in events. 

__Example:__

```c#
public delegate void LogMessageEventHandler(string message);
public static event LogMessageEventHandler OnLogMessage;
```

__BAD:__

```c#
public delegate void Click()
```
__GOOD:__

```c#
public delegate void ClickEventHandler()
```
DO add the suffix __Callback__ to names of delegates other than those used as event handlers.

__BAD:__

```c#
public delegate void Render()
```
__GOOD:__

```c#
public delegate void RenderCallback()
```
### Events

Prefix event functions with the prefix __On__.

__BAD:__

```c#
public static event CloseCallback Close;
```
__GOOD:__

```c#
public static event CloseCallback OnClose;
```

### Coroutines

Coroutines are written __UpperCamelCase__.

When declaring coroutines, DO add the suffix __Thread__. 

Coroutines should __always be private__. Use regular functions as wrappers when necessary.

__BAD:__

```c#
public Coroutine renderStuff()
```
__GOOD:__

```c#
private Coroutine RenderCallbackThread()
```

### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```c#
XMLHTTPRequest
String URL
findPostByID
```
__GOOD:__

```c#
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for all classes, functions and
member variables.

__BAD:__

```c#
string word 
int id;
```

__GOOD:__

```c#
protected string word 
private int id;
```
### Fields & Variables

Prefer single declaration per line.

__BAD:__

```c#
private string username, twitterHandle;
```

__GOOD:__

```c#
private string username;
private string twitterHandle;
```

### Classes

Generally keep to one class per source file, except for tiny struct-like classes used in the 
main class of a source file.

### Interfaces

All interfaces should be prefaced with the letter __I__. 

__BAD:__

```c#
RadialSlider
```

__GOOD:__

```c#
IRadialSlider
```

### Enums

Enums should always be declared inline.

__BAD:__

```c#
enum Days {
    Sat, 
    Sun, 
    Mon, 
    Tue, 
    Wed, 
    Thu, 
    Fri
};
```

__GOOD:__

```c#
enum Days {Sat, Sun, Mon, Tue, Wed, Thu, Fri};
```

## Spacing

### Indentation

Always indent - never spaces.

### Line Length

Lines should be no longer than 150 characters. If a line exceeds 150 characters you should start a new line. Ideally, lines which break should do so after an operator (=, < etc).

There should always be a single indent on the new line when a line is broken up in this manner.

__BAD:__

```c#
int a = 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1;
```

__GOOD:__

```c#
int a = 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 
    1 + 3 + 1 + 1 + 3 + 1 + 1 + 3 + 1;
```


### Vertical Spacing

There should be exactly one blank line between functions to aid in visual clarity 
and organization. Whitespace within functions should separate functionality, but 
having too many sections in a functions often means you should refactor into
several methods.


## Brace Style

+	The opening-braces for Classes and functions get their own lines.
+	All other opening-braces -- ifs, elses, etc. -- should be on the same line as the preceding statement.
+	Trailing closing-braces always get their own line.
+	Elses and else-ifs get their own line

__BAD:__

```c#
class MyClass{
  void DoSomething(){
    if (someTest)
    {
      // ...
    } else
    {
      // ...
    }
  }
}
```

__GOOD:__

```c#
class MyClass 
{
  void DoSomething() 
  {
    if (someTest) {
      // ...
    } 
	else {
      // ...
    }
  }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

__BAD:__

```c#
if (someTest)
  doSomething();
if (someTest) doSomethingElse();
```

__GOOD:__

```c#
if (someTest) {
  doSomething();
}
if (someTest) { doSomethingElse(); }
```


## Switch Statements

Switch statements fall-through by default, but this can be unintuitive. Do not use fall-through behavior. 

Alway include the `default` case.

## Commenting

###Classes & Functions

Classes and functions that see heavy use should have a Visual Studio ```<summary>``` comment directly above their declarations. This will create a Visual Studio tooltip explaining to other members of our team what the function does. If the function can be described in one line, this comment should be inline. If the description is longer than a line, this comment can span multiple lines. For these comments to work they must be proceeded by ```///``` instead of just ```//```.

__Inline Example:__

```c#
///<summary>Comment goes here.</summary>
public void HasATooltip(){

}
```

__Multi-line Example:__

```c#
///<summary>
///Comment goes here.
///Second comment does here.
///</summary>
public void HasATooltip(){

}
```

###Fields

Unless it is explicitly clear what a field does, it should have an inline comment explaining what it does. These comments should be formatted to be clear to read as you go down the document. 

__BAD:__

```c#
public int variableA;               //A variable
public int variableB;       //Not a useful comment
public int variableC;
public Rigidbody mRigidbody;        //My rigid body
```

__GOOD:__

```c#
public int variableA;               //Start point of movement lerp
public int variableB;               //End point of movement lerp
public int variableC;               //Lerp amount
public Rigidbody mRigidbody;
```


## Unity Editor

When assigning references to other components and GameObjects from a script, do as much as possible to avoid assigning references in the inspector. Whenever possible, use ```GetComponent``` or the getters on a service to get your references

The name of a GameObject should ​_never_​ matter -- reserve names for labeling and organization! This means that ```GameObject.Find``` is ​_banned._​

Whenever possible, the ​_hierarchical order_​ of gameobjects should not matter. The one exception is the order of Canvas children, where the order is used for Z-indexes.

###Exposed Variables

For every component, only variables ​_we actively want to tweak_​ should ever be exposed to the inspector. All others should use ```private```, ```protected```, or ```[HideInInspector]```

If a variable should be ```private``` but needs to be edited in inspector, you should declare it as private and mark it with ```[SeralizedField]``` 

*Variables should only be public if other scripts need to reference them*.

__BAD:__

```c#
public int doesNotNeedToBePublic;
```

__GOOD:__

```c#
[SerializeField] private int doesNotNeedToBePublic;
```

###SceneManager Organization

Grassdancer uses Unity's new SceneManager to break up scenes in order to make it easy for our team to work on the same scene at the same time. As the scenes in our project will be organized first by what level they are and then by what part of the level they are. 

The different levels are:

- PlayerScene (The only "level" not broken up into parts. All global objects should go here)
- Hub
- R1
- R2
- R3

The different parts of each level (excluding PlayerScene) are:

- Audio
- Decorative
- GameplayGeo
- NPCs

Scenes are all __UpperCamelCase__ and are named "LevelName" + "PartName" and should be saved under Assets/_Scenes/"LevelName"

__BAD:__

```c#
R1_Audio.unity
```

__GOOD:__

```c#
R1Audio.unity
```

## GameManager & Services

Grassdancer only has one singleton, called 'GameManager', which contains a variety of Services. These services can be referenced by other scripts independently of one another and function as modular parts of the singleton. The purpose of this is to have a system that only uses one singleton but is still highly modular and efficient. 

### Accessing a Service

To access a service in a script you first must make a reference to the desired service. To do so, you first declare a private interface with a type matching the type of the desired service. 

```c# 
private IDesiredService desiredManager
```

Then in Start(), you set the reference through 

```c# 
desiredManager = GameManager.Getservice(typeof(IDesiredService)) as IDesiredService
```

Once this has been done you can use the service as needed. 

### Creating a Service

There are three parts to creating a service. 

First, you need to create an interface. This interface functions similarly to a .h file in C++ in that it prototypes the functions that will be implemented in the Service itself. All Interfaces used in conjunction with a Service should be saved in Assets/Scripts/GameManagers/ServiceInterfaces.

This is what makes our system modular, as it will allow for an engineer to change whatever they want (outside of a few things like parameters) to the service itself without affecting any of the other scripts that reference it. *Note that unlike a .h file in C++, everything declared in an Interface must be public. If you need private variables declare and instantiate them in the Service itself*

__Example:__

```c#
public interface IAudioService
{
    ///<summary>Plays a 2D Sound</summary>
    void Play2DSound(string soundName, float volume = 1f);
    ///<summary>Plays a 3D Sound</summary>
    void Play3DSound(string soundName, Vector3 position, float volume = 1f);
}
```

Second, you need to create the service. A service should inherit from both MonoBehaviour and the interface that it is attached to. The service should implement everything declared in its Interface as well as any functionality that is needed for the service to work, but isn't necessarily needed by the scripts that will reference the service. Services should be saved to Assets/Scripts/GameManagers/Services.

__Example:__

```c#
public class AudioManager : MonoBehaviour, IAudioService
{
    public void Play2DSound(string soundName, float volume = 1f)
    {
        //Implementation goes here
    }

    public void Play3DSound(string soundName, Vector3 position, float volume = 1f)
    {
        //Implementation goes here
    }
}
```

Finally, once your service is created and functional, you need to register it to the ServiceContainer on GameManager so other scripts can access it. To do so you must add the following lines of code to the GameManager's InitializeServices function. (replace IAudioService with the name of your interface and AudioManager with the name of your service)

```c#
    IAudioService audioService = gameObject.AddComponent<AudioManager>();
    services.RegisterService(typeof(IAudioService), audioService);
```

This instantiates the service and adds it to the ServiceContainer, which allows other scripts to access it through GetService);

## Credits

The original version of this style guide was a collaborative effort from the most stylish
raywenderlich.com team members:

- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Brian Moakley](https://github.com/VegetarianZombie)
- [Ray Wenderlich](https://github.com/rwenderlich)

The version you are reading was put together by the Sugarscape team:

- [Will Anderson](https://twitter.com/regularfriend)
- [Brendan LoBuglio](https://twitter.com/BrendanLoBuglio)
- [Chloe Lister](https://twitter.com/chlolist)
- [Lex Rhodes](https://twitter.com/upsetspacecadet)
- [Ryan Bobell](https://twitter.com/RyanBobell)
- Jonathan Bodian