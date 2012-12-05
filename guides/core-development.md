# Pender Development
developing with Pender Native

## terminology
- client
any time the docs says client, it means your code which uses pender api's

## Project Setup
see the Getting Started (getting-started.md) guide

## How Pender Works
Pender provides a domless JavaScript runtime for the efficient execution of javascript code. Regardless of platform:

- Pender instantiates a JavaScript virtual machine embedded in the native runtime. 
Specifically, this a Rhino JSVM is created in an OpenGL Renderer Thread 
- Pender packages and injects various native classes into the JSVM, exposing the Pender API to javascript executing in this context
Theses inculde the hooks your client js application uses to communicate. This also includes functionality that exists in a browser environment, like the Canvas api.
- Pender executes a per frame update of the js context in the onDraw function of an openGL renderer in the renderer thread
any timed functions you have registered in the regular javascript ways (setTimeout, setInterval, requestAnimationFrame, etc) will be executed as per their specific arguments

## Important Native Classes

### PenderJS.java
see the docs/api documments for more information

PenderJS.java is a JavaScript facing api implemented in Java. This means that PenderJS.java is injected into a javascript context, allowing client javascript to interact with native code.

PenderJS.java implements the essential JS API that a pender client app expects

### PenderCanvas.java
Another central class, this implements the HTML5 Canvas api exposed to the pender javascript runtime

## Running Tests

## Quirks

* current version of Pender is based as a Android project. You must include and run the PenderActivity.java as your main activity in order to use pender.

