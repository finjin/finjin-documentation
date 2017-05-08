## Design

```
This documentation is preliminary.
```

\section design_overview_subsystems Subsystems

The subsystems within the engine are organized by functionality.

* *GPU* - Graphics and compute.
  * *D3D12System* - Direct3D 12 GPU system. Used on Windows 10 (Win32 and UWP).
  * *VulkanSystem* - Vulkan GPU system. Used on Windows 7, Windows 8, Windows 10 (Win32), Linux, and Android.
  * *MetalSystem* - Metal GPU system. Used on iOS, tvOS, and macOS.
* *Input* - Input devices - keyboards, mice, and game controllers.
  * *AndroidInputSystem* - Used on Android.
  * *IOSInputSystem* - Used on iOS and tvOS.
  * *LinuxInputSystem* - Used on Linux.
  * *MacOSInputSystem* - Used on MacOS.
  * *WindowsUWPInputSystem* - Used on Windows 10 (UWP).
  * *Win32InputSystem* - Used on Windows 7, Windows 8, and Windows 10 (Win32).
* *Sound* - Sound/music.
  * *AVAudioEngine* - Used on iOS, tvOS, and macOS.
  * *OpenALSystem* - Used on Linux.
  * *OpenSLESSystem* - Used on Android.
  * *XAudio2System* - Used on Windows.
* *VR* - Virtual reality devices and output.
  * *OpenVRSystem* - Used with OpenVR on Windows (Win32).


\section design_overview_subsystem_contexts Subsystem Contexts

A *context* is created for an application window and provides access to a particular subsystem. An application window has one context for each subsystem.

During the initialization phase, the *Create()* method of each context is called. If there is a critical failure, the creation aborts, *Destroy()* is called on each context, and then the application exits, likely with an error being displayed.

The *Create()* phase of each context operates as follows:
* Create() will be called exactly once during the application initialization phase.
* Resources are enumerated and preallocated according to configuration and the current execution environment.
* If there is a critical failure:
  * The creation aborts with error information.
  * Resources that were allocated - but didn't fail - do not need to be destroyed. They will be destroyed later.

The *Destroy()* phase of each context operates as follows:
* Destroy() will be called exactly once during the application shutdown phase.
* It is acceptable to let resources implicitly destroy themselves if they can do so correctly (such as with smart pointers and destructors that get called when the context is 'delete'ed). Otherwise, resources should be explicitly destroyed.
* Non-resource and simple values (such as counters, timestamps, etc.) do not need to be reset.
* No errors are recorded during this phase.
