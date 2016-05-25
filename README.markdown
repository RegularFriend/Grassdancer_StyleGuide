# The Official Grassdancer C# Style Guide

Our overarching goals are __conciseness__, __readability__ and __simplicity__. Also, this guide is written to keep Unity in mind. 

## Inspiration

This style-guide is somewhat of a mash-up between the existing C# language
style guides, and a tutorial-readability focused Swift style-guide. guide). This style guide was created from the Java style guide and then altered from various C# / Unity style guides across the web.

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Script Files](#script-files)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Coroutines](#coroutines)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classe)
  + [Interfaces](#interfaces)
  + [Enums](#Enums)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Commenting](#commenting)
- [Unity Editor](#unity-editor)
  + [Exposed Variables](#exposed-variables)
- [Credits](#credits)


## Nomenclature

On the whole, naming should follow C# standards.

### Script Files

Script files are all __UpperCamelCase__, multiple words concatenated together,
without
hypens or underscores:

__BAD__:

```c#
game_Manager.cs
```

__GOOD__:

```c#
GameManager.cs
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example `RadialSlider`. 

### Functions

Public functions are written in __UpperCamelCase__. For example `DoSomething`. 

Private functions are written in __lowerCamelCase__. For example: `doSometing`

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

Prefix event methods with the prefix __On__.

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

When declaring delegates, DO add the suffix __Thread__. 

Coroutines should __always be private__. Use regular functions as wrappers when necessary.

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

Access level modifiers should be explicitly defined for classes, methods and
member variables.

__BAD:__

```c#
string word 
int Id;
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
string username, twitterHandle;
```

__GOOD:__

```c#
string username;
string twitterHandle;
```

### Classes

Exactly one class per source file, except for tiny struct-like classes used in the 
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
enum Days {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

## Spacing

### Indentation

Always indent - never spaces.

### Line Length

Lines should be no longer than 150 characters. If a line exceeds 150 characters you should start a new line. Ideally lines will end after an operator (=, < ect).

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

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.


## Brace Style

+	The opening-braces for Classes and functions get their own lines.
+	All other opening-braces -- ifs, elses, etc. -- should be on the same line as the preceding statement.
+	Trailing closing-braces always get their own line.
+	Else gets its own line

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

Will have commenting spec here

## Unity Editor

When assigning references to other components and GameObjects from a script, do as much as possible to avoid assigning references in the inspector. Whenever possible, use ```GetComponent``` or the getters on a singleton to get your references

The name of a GameObject should ​_never_​ matter -- reserve names for labeling and organization! This means that ```GameObject.Find``` is ​_banned._​

Whenever possible, the ​_hierarchical order_​ of gameobjects should not matter. The one exception is the order of Canvas children, where the order is used for Z-indexes.

###Exposed Variables

-	For every component, only variables ​_we actively want to tweak_​ should ever be exposed to the inspector. All others should use ```private```, ```protected```, or ```[HideInInspector]```
   + If a variable should be ```private``` but needs to be edited in inspector, you should declare it as private and mark it with ```[SeralizedField]``` *Variables should only be public if other scripts need to reference them*.

__BAD:__

```c#
public int doesNotNeedToBePublic;
```

__GOOD:__

```c
[SerializedField]
private int editInInspector
```

###SceneManager Organization

stuff will be here eventually

## Credits

This style guide is a collaborative effort from the most stylish
raywenderlich.com team members:

- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Brian Moakley] (https://github.com/VegetarianZombie)
- [Ray Wenderlich](https://github.com/rwenderlich)

As well as the Sugarscape engineers

- Will Anderson
- Brendan LoBuglio
- Chloe Lister