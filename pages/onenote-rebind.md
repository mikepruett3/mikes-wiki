# [Changing the OneNote Screen Clipping and New Side Note keyboard shortcuts](https://blogs.msdn.microsoft.com/descapa/2006/11/17/changing-the-onenote-screen-clipping-and-new-side-note-keyboard-shortcuts/)

I think this is the longest title for a post yet. Have you wanted to change the keyboard shortcut for screen clippings? For new side notes? For a new screen clipping? This is the question that was asked in our internal DL:

*I wanted to get a screen capture of something while I was mouse clicking on something but I could not click the mouse and be able to stretch the fingers on my other hand to reach both the Windows + S key.  Can I assign a different letter than S which is closer to the Windows key?*

Now @ first glance you might think that S and the Windows key are close together, but if you have Toshiba laptop they decided to put the Windows key on the top right of the keyboard (which totally pissed me off for the first month of use). So actually in OneNote you can change this via the registry, here are the steps. Note: you can only do this with OneNote 2007.

By default OneNote uses "s" for screen clipping and "n" for new side note. You can change that by changing the following reg keys under this path:

```Registry
HKEY_CURRENT_USER\Software\Microsoft\Office\12.0\OneNote\Options\Other
```

There are two DWORD values **ScreenClippingShortcutKey** & **NewNoteShortcutKey**. The default values are:

| Keys | Values |
|:---|---|
| ScreenClippingShortcutKey | 0x53|
| NewNoteShortcutKey | 0x4e |

Now this might not make sense but those are hex values for the keyboard keys, here is an entire mapping:


| Key | Dec | Hex |
|---|---|---|
| a | 65 | 41 |
| b | 66 | 42 |
| c | 67 | 43 |
| d | 68 | 44 |
| e | 69 | 45 |
| f | 70 | 46 |
| g | 71 | 47 |
| h | 72 | 48 |
| i | 73 | 49 |
| j | 74 | 4A |
| k | 75 | 4B |
| l | 76 | 4C |
| m | 77 | 4D |
| n | 78 | 4E |
| o | 79 | 4F |
| p | 80 | 50 |
| q | 81 | 51 |
| r | 82 | 52 |
| s | 83 | 53 |
| t | 84 | 54 |
| u | 85 | 55 |
| v | 86 | 56 |
| w | 87 | 57 |
| x | 88 | 58 |
| y | 89 | 59 |
| z | 90 | 5A |

Say for example you wanted the screen clipping command to be Win+P instead of Win+S, just create a new DWORD called ScreenClippingShortcutKey and give it the value of 0x50. Now just log off/log on and you should be all set!

I hope this helps you all if you questions please let me know. Also if someone wants to make a nice GUI app that does this that would be awesome too J Maybe I should but just not enough time.