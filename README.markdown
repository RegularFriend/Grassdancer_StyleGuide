# The Official Grassdancer C# Style Guide

Our overarching goals are __conciseness__, __readability__ and __simplicity__. Also, this guide is written to keep Unity in mind. 

## Inspiration

This style-guide is somewhat of a mash-up between the existing C# language
style guides, and a tutorial-readability focused Swift style-guide. guide). This style guide was created from the Java style guide and then altered from various C# / Unity style guides across the web.

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Copyright Statement](#copyright-statement)
- [Smiley Face](#smiley-face)
- [Credit](#credits)


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

## Spacing

### Indentation

Always indent - never spaces.

### Line Length

Lines should be no longer than 100 characters long.


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


## Singleton Style
Singleton.cs is a script we will use to define singleton behavior. All singletons will inherit from this class.

__Singleton.cs__
```c#
using UnityEngine;
 
/// <summary>
/// Be aware this will not prevent a non singleton constructor
///   such as `T myT = new T();`
/// To prevent that, add `protected T () {}` to your singleton class.
/// 
/// As a note, this is made as MonoBehaviour because we need Coroutines.
/// </summary>
public class Singleton<T> : MonoBehaviour where T : MonoBehaviour
{
	private static T _instance;
	private static object _lock = new object();
	protected static T Instance
	{
		get{
			if (applicationIsQuitting) {
				Debug.LogWarning("[Singleton] Instance '"+ typeof(T) +
					"' already destroyed on application quit." +
					" Won't create again - returning null.");
				return null;
			}
 
			lock(_lock){
				if (_instance == null){
					_instance = (T) FindObjectOfType(typeof(T));
 
					if ( FindObjectsOfType(typeof(T)).Length > 1 ){
						Debug.LogError("[Singleton] Something went really wrong " +
							" - there should never be more than 1 singleton!" +
							" Reopening the scene might fix it.");
						return _instance;
					}
 
					if (_instance == null)
					{
						GameObject singleton = new GameObject();
						_instance = singleton.AddComponent<T>();
						singleton.name = "(singleton) "+ typeof(T).ToString();
 
						DontDestroyOnLoad(singleton);
 
						Debug.Log("[Singleton] An instance of " + typeof(T) + 
							" is needed in the scene, so '" + singleton +
							"' was created with DontDestroyOnLoad.");
					} else {
						Debug.Log("[Singleton] Using instance already created: " +
							_instance.gameObject.name);
					}
				}
 
				return _instance;
			}
		}
	}
 
	private static bool applicationIsQuitting = false;
	/// <summary>
	/// When Unity quits, it destroys objects in a random order.
	/// In principle, a Singleton is only destroyed when application quits.
	/// If any script calls Instance after it have been destroyed, 
	///   it will create a buggy ghost object that will stay on the Editor scene
	///   even after stopping playing the Application. Really bad!
	/// So, this was made to be sure we're not creating that buggy ghost object.
	/// </summary>
	public void OnDestroy () {
		applicationIsQuitting = true;
	}
}
```
__Declaration:__

```c#
public class Manager : Singleton<Manager> 
{
	protected Manager () {} // guarantee this will be always a singleton only - can't use the constructor!
	public string myGlobalVar = "whatever";
}
```

__Unity reference:__
http://wiki.unity3d.com/index.php?title=Singleton


## Unity Editor

__Exposed Variables__

+	For every component, only variables ​_we actively want to tweak_​ should ever be exposed to the inspector. All others should use ```private```, ```protected```, or ```[HideInInspector]```
+	When assigning references to other components and GameObjects from a script, do as much as possible to avoid assigning references in the inspector. Whenever possible, use ```GetComponent``` or the getters on a singleton to get your references
+	The name of a GameObject should never matter.
+	The order of GameObjects in the heirarchy should never matter except in the case of UI.