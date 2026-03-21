---
layout: post
title: "Quickshell"
date: 2026-03-21
categories: Linux Sofware Ricing
---

I find enjoyment in customising the graphical shell when I use Linux.
This has lead me to different technologies and many rewrites of my shell,
each getting more custom and polished than the last.
I started with [Polybar](https://github.com/polybar/polybar) -- a classic,
then [Eww](https://github.com/elkowar/eww) -- which proved the market for highly customisable shells,
then [Ironbar](https://github.com/JakeStanger/ironbar) -- to tide me over the wayland changes,
then a go at building something from scratch -- [MCW](https://github.com/CMurtagh-LGTM/murts-cool-widgets),
now currently I'm on [Quickshell](https://github.com/quickshell-mirror/quickshell).

Quickshell is a Qt based toolkit for making desktop shells for Wayland
developed by outfoxxed.
You use [QML](https://doc.qt.io/qt-6/qmlapplications.html) to define the graphical shell.
Here's a quick example of my bar written QML:

``` qml
import QtQuick
import Quickshell

Scope {
  Variants {
    model: Quickshell.screens

    PanelWindow {
      property var modelData
      screen: modelData

      anchors {
        top: true
        left: true
        right: true
      }
      aboveWindows: false

      implicitHeight: 30

      color: "#00000000"

      Rectangle {
        height: 3
        width: parent.width
        anchors.bottom: parent.bottom
        color: "{{bg_dim}}"
      }

      Workspaces {
        anchors.left: parent.left
      }

      ClockWidget {
        anchors.horizontalCenter: parent.horizontalCenter
      }

      Tray {
        id: tray
        anchors.right: parent.right
      }
      Mpris {
        anchors.right: tray.left
      }
    }
  }
}
```

As you can see it is a clear and concise way of defining a GUI.
I like how each object is defined in a hierarchical order and properties of each object can be referenced cleanly.
It isn't perfect though, for example the inbuilt scripting uses a feature lacking and non-complaint implementation of JavaScript
-- an already bottom of the barrel language.

## Shell Components

I try to achieve a clean and simple graphical shell only with information that I need to access regally
but with plenty of animations to add juice.
If you are interested at looking at the QML it is currently located in my [dotfiles repo](https://github.com/CMurtagh-LGTM/dots).

### Bar

![Bar](/assets/images/quickshell/bar.jpg)

![Calendar](/assets/images/quickshell/calendar.jpg)

As you can see this bar looks quite similar to how Ironbar can look.
Even though I could get Ironbar to nearly what I wanted,
I feel was is well worth investing time into writing it again in Quickshell.

Compared to doing everything myself from scratch,
being able to use existing components makes Quickshell relatively quick to set up.
For example in my bar I used:
[Workspaces](https://quickshell.org/docs/master/types/Quickshell.Hyprland/HyprlandWorkspace/),
[Mpris](https://quickshell.org/docs/master/types/Quickshell.Services.Mpris/MprisPlayer) and
[System Tray](https://quickshell.org/docs/master/types/Quickshell.Services.SystemTray/SystemTrayItem/)
and got a bar working in a few hours
whilst these three things took weeks to achieve when I was trying to do everything from scratch.

### Launcher

![Launcher](/assets/images/quickshell/launcher.png)

My launcher is the standard [Wofi](https://hg.sr.ht/~scoopta/wofi) style of fuzzy search drop down.
The only real reason I decided to write this in Quickshell is to make sure all my shell components have a similar visual style.

Instead of implementing a fuzzy finding algorithm in JavaScript I created a [Patch](https://github.com/quickshell-mirror/quickshell/pull/188)
that implemented it in C++ instead.

### Notification Window

![Notify](/assets/images/quickshell/notify.jpg)

A [Dunst](https://github.com/dunst-project/dunst) clone for same reasons as above.

### Logout

![Logout](/assets/images/quickshell/logout.png)

A copy of the outfoxxed's [example](https://git.outfoxxed.me/quickshell/quickshell-examples/src/branch/master/wlogout).

### On Screen Display

![OSD](/assets/images/quickshell/osd.jpg)

A copy of the outfoxxed's [example](https://git.outfoxxed.me/quickshell/quickshell-examples/src/branch/master/wlogout).

## A Failed Emoji Picker

I tried to make a Emoji picker like the one found in windows in this [PR](https://github.com/quickshell-mirror/quickshell/pull/195).
To achieve this I tried to utilize the [Input Method](https://en.wikipedia.org/wiki/Input_method) Wayland protocol.
However I came against some problems as described by DorotaC in [State of input method](https://dorotac.eu/posts/input_broken/).
I don't have any ideas on how to fix these issues nor do I want to enter the maelstrom that is the Wayland protocol discussions,
so this patch has unfortunately been put on hold -- possibly indefinitely.

## Conclusion

Currently I think that Quickshell is the best toolkit for creating custom graphical shells.
The space is always evolving and there may be an even better toolkit in the future.
What a joy it is to be a part of this community.

