## Finjin Engine

```
This documentation is preliminary.
```

\section engine_about About

The Finjin engine provides the core functionality for applications.

\section engine_features Features
* Creates application windows.
* Implements the main application loop.
* Provides a multithreaded job system for distributing work across multiple CPU cores.
* Provides readers for streaming in scene data.
* And more...

\section engine_supported_platforms Supported Operating Systems / Platforms

| Operating System / Platform      | Graphics System | Sound System     | Input System                                        | Special Notes                                                 |
| :------------------------------: | :-------------: | :--------------: | :-------------------------------------------------: | :-----------------------------------------------------------: |
| Android 6+                       | Vulkan          | OpenSL ES        | Standard window input                               | Multiple windows not available.                               |
| iOS 10+                          | Metal           | AVAudioEngine    | Standard window input and Game Controller framework | Multiple windows not available.                               |
| Linux                            | Vulkan          | OpenAL           | Standard window input                               |                                                               |
| macOS 10+                        | Metal           | AVAudioEngine    | Standard window input and Game Controller framework |                                                               |
| tvOS 10+                         | Metal           | AVAudioEngine    | Standard window input and Game Controller framework | Multiple windows not available.                               |
| Windows 7, 8.1                   | Vulkan          | XAudio2          | XInput and DirectInput                              |                                                               |
| Windows 10 / UWP                 | D3D12           | XAudio2          | Standard window input and XInput                    | Multiple windows not available.                               |
| Windows 10 / Win32               | D3D12 or Vulkan | XAudio2          | XInput and DirectInput                              | D3D12 and Vulkan versions are separate executables.           |

\section engine_dev_target_tools Development Target Tools

* All targets:
  * Python 3.x - Some utilities are written in Python.

| Target                           | Development Platform | Development Environment            | Additional Software                                                                              | Special Notes                                                                |
| :------------------------------: | :------------------: | :--------------------------------: | :----------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------: |
| Android                          | Windows              | Visual Studio 2015 with Update 3   | [NVidia CodeWorks for Android (External link)](https://developer.nvidia.com/gameworksdownload)   | Applications must be run on target device, not the simulator.                |
| iOS / macOS / tvOS               | macOS                | XCode 8                            |                                                                                                  | Applications must be run on target device, not the simulator.                |
| Linux                            | Linux                | NetBeans 8.1                       |                                                                                                  |                                                                              |
| Windows / UWP                    | Windows 10           | Visual Studio 2015 with Update 3   |                                                                                                  | Applications must be run on target device, not the simulator.                |
| Windows / Win32                  | Windows 7 and higher | Visual Studio 2015 with Update 3   |                                                                                                  |                                                                              |


	
\section engine_conventions Conventions

\subsection engine_coordinate_system Coordinate System
The Finjin exporter and engine use a right-handed coordinate system with the up axis pointing along the Y (0, 1, 0) axis, and the Z axis pointing toward the viewer.

\subsection engine_memory_size Memory Size
When specifying memory size in text, such as in a configuration file, the following suffixes may be used:

| Unit Name         | Number of Bytes                       | Suffixes (short, singular, plural)          | Examples                             |
| :---------------: | :-----------------------------------: | :-----------------------------------------: | :----------------------------------: |
| Byte              | 1                                     | B, byte, bytes                              | 3B, 3byte, 3bytes                    |
| Kilobyte          | 1,000                                 | KB, kilobyte, kilobytes                     | 3KB, 3kilobyte, 3kilobytes           |
| Kibibyte          | 1,024                                 | KiB, kibibyte, kibibytes                    | 3KiB, 3kibibyte, 3kibibytes          |
| Megabyte          | 1,000,000 (1,000 x 1,000)             | MB, megabyte, megabytes                     | 3MB, 3megabyte, 3megabytes           |
| Mebibyte          | 1,048,576 (1,024 x 1,024)             | MiB, mebibyte, mebibytes                    | 3MiB, 3mebibyte, 3mebibytes          |
| Gigabyte          | 1,000,000,000 (1,000 x 1,000 x 1,000) | GB, gigabyte, gigabytes                     | 3GB, 3gigabyte, 3gigabytes           |
| Gibibyte          | 1,073,741,824 (1,024 x 1,024 x 1,024) | GiB, gibibyte, gibibytes                    | 3GiB, 3gibibyte, 3gibibytes          |

\subsection engine_time_duration Time Duration
When specifying time duration in text, such as in a configuration file, the following suffixes may be used:

| Unit Name         | Suffixes (short, singular, plural)          | Examples                                             |
| :---------------: | :-----------------------------------------: | :--------------------------------------------------: |
| Nanosecond        | ns, nanosecond, nanoseconds                 | 3ns, 3nanosecond, 3nanoseconds                       |
| Microsecond       | us, microsecond, microseconds               | 3us, 3microsecond, 3microseconds                     |
| Millisecond       | ms, millisecond, milliseconds               | 3ms, 3millisecond, 3milliseconds                     |
| Second            | s, second, seconds                          | 3s, 3second, 3seconds                                |
| Minute            | m, minute, minutes                          | 3m, 3minute, 3minutes                                |
| Hour              | h, hour, hours                              | 3h, 3hour, 3hours                                    |



\section engine_file_formats File Formats

\subsection engine_finjin_file_formats Finjin File Formats

| Name                                                               | Extension | Encoding     | Line Ending           | Reader Memory Usage                                                | Best Use                                                              | Related Classes                                                                                                                                          | Special Notes                                                                                                                                                                                                                   |
| :----------------------------------------------------------------: | :-------: | :----------: | :-------------------: | :----------------------------------------------------------------: | :-------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Finjin Streaming Binary Document                                   | .fsbd     | Binary       | Not applicable        | One data line - Up to *max-bytes-per-line*, as defined in the file | Most assets - production                                              | Finjin::Common::BinaryDataChunkReader, Finjin::Common::BinaryDataChunkWriter                                                                             | 1)When generating assets with the Finjin exporters, this is the preferred file format. 2)Ensure your source control system treats this file type as a binary file.                                                              |
| Finjin Streaming Text Document                                     | .fstd     | Text / UTF-8 | \\n                   | One data line - Up to *max-bytes-per-line*, as defined in the file | Most assets - development and archiving                               | Finjin::Common::TextDataChunkReader, Finjin::Common::TextDataChunkWriter                                                                                 | 1)Ensure your source control system doesn't alter line endings for this file type. 2)A data line may contain multiple newline characters.                                                                                       |
| <a href="#engine_extended_config_file_format">Extended Config</a>  | .cfg      | Text / UTF-8 | \\r\\n or \\n         | Entire file                                                        | Configuration files that can be written and modified by hand          | Finjin::Common::ConfigDataChunkReader, Finjin::Common::ConfigDataChunkWriter, Finjin::Common::ConfigDocumentReader, Finjin::Common::ConfigDocumentWriter | 1)The writer writes \\n, but the reader reads \\r\\n or \\n. 2)This is the only file format that can be written by hand.                                                                                                        |
| JavaScript Object Notation (JSON)                                  | .json     | Text / UTF-8 | \\r\\n or \\n         | One data line - Up to the size of the longest line in the file     | Assets that can be read by a standard JSON parser outside the engine  | Finjin::Common::JsonDataChunkReader, Finjin::Common::JsonDataChunkWriter                                                                                 | 1)The writer writes \\n, but the reader reads \\r\\n or \\n. 2)JsonDataChunkWriter or the Finjin exporters must be used to create these files (not an external JSON writer) due to specific formatting requirements.            |
| Texture                                                            | .texture  | Binary       | Not applicable        | Entire file                                                        | Textures                                                              | Finjin::Common::WrappedFileReader, Finjin::Common::WrappedFileWriter                                                                                     | 1)This file contains an embedded texture file. The texture file format must be supported to load successfully. 2)WrappedFileWriter, wrap_file.py, or the Finjin exporters must be used to create these files.                   |
| Sound                                                              | .sound    | Binary       | Not applicable        | Entire file                                                        | Sounds                                                                | Finjin::Common::WrappedFileReader, Finjin::Common::WrappedFileWriter                                                                                     | 1)This file contains an embedded sound file. The sound format must be supported to load successfully. 2)WrappedFileWriter, wrap_file.py, or the Finjin exporters must be used to create these files.                            |

\subsection engine_external_file_formats External File Formats

| Name                                             | Extension | Encoding     | Line Ending           | Reader Memory Usage           | Best Use             | Related Classes                   | Supported By                                  |
| :----------------------------------------------: | :-------: | :----------: | :-------------------: | :---------------------------: | :------------------: | :-------------------------------: | :-------------------------------------------: |
| Adaptive Scalable Texture Compression (ASTC)     | .astc     | Binary       | Not applicable        | Entire file                   | Textures             | Finjin::Engine::ASTCReader        | Vulkan graphics system                        |
| DirectDraw Surface (DDS)                         | .dds      | Binary       | Not applicable        | Entire file                   | Textures             | Finjin::Engine::DDSReader         | D3D12 graphics system                         |
| Khronos Texture (KTX)                            | .ktx      | Binary       | Not applicable        | Entire file                   | Textures             | Finjin::Engine::KTXReader         | Vulkan graphics system                        |
| Portable Network Graphics (PNG)                  | .png      | Binary       | Not applicable        | Entire file                   | Textures             | Finjin::Common::PNGReader         | All graphics systems                          |
| Waveform Audio (WAV)                             | .wav      | Binary       | Not applicable        | Entire file                   | Sound effects        | Finjin::Engine::WAVReader         | All sound systems                             |

\subsection engine_texture_formats Texture Formats

| Name                                             | Supported External File Formats   | Supported Rendering System                    |
| :----------------------------------------------: | :-------------------------------: | :-------------------------------------------: |
| Adaptive Scalable Texture Compression (ASTC)     | ASTC                              | If hardware supports it: Vulkan               |
| Ericsson Texture Compression (ETC2)              | KTX                               | If hardware supports it: Vulkan               |
| Block Compression (BC 4, 5, 6, 7)                | DDS, KTX                          | If hardware supports it: D3D12, Vulkan        |
| Portable Network Graphics (PNG)                  | PNG                               | All graphics systems                          |

\subsection engine_extended_config_file_format Extended Config (.cfg) File Format

The extended .cfg format is often used for handwritten configuration files, such as those for input devices and input bindings. Features and conventions:
* *Extends the standard format by allowing nested sections and multiline values* - This simplifies the process of describing complex data.
* *Leading tabs are preferred over spaces* - Tabs use less space, which is important since .cfg files are read completely into memory before being parsed.
* *Multiline values are allowed* - No special escaping within the text value is necessary. See the example below for the multiline syntax.
* *Trailing value whitespace is ignored* - A line with "key=value             " (without quotes) is equivalent to "key=value" (without quotes).

### Example

```
#This is a comment. Comments must be on their own line.
some-key=some value
[section]
{	
	another-key=Another value
	
	#Another comment
	[nested-section]
	{
		key=single line value
		key^=multi 
line 
value
^
	}
}
```

\section engine_workflow Asset Creation Workflow

\subsection engine_workflow_basic Basic Workflow

1. Create a scene in 3DS Max or Maya.
  * Only .png format images should be used as textures in materials in 3DS Max / Maya.
2. Modify settings.
  * Settings are accessible through the Finjin menu, which is part of the main menu in 3DS Max and Maya. Global, scene, and object settings are available.
    * *Global settings* are loaded when 3DS Max / Maya starts, and applied the same across all exports.
    * *Scene settings* are part of a 3DS Max / Maya file, and are applied to the scene during the export of that file.
    * *Object settings* are part of a 3DS Max / Maya file, and are applied to an object during the export of that file. 
  * For a simple scene no settings modification is necessary.
3. Export the data.
  * The export can be performed through the standard means in 3DS Max / Maya, or through the Finjin *Export* menu. 
  * By default meshes, lights, cameras, materials, and textures will be exported.
  * The data will be exported into an <a href="#engine_asset_directory_structure">asset directory structure</a>.
  * Textures will be converted into .texture files. If necessary, these can be unwrapped using *wrap_file.py* in finjin-common/tools.
4. Load the data into your application or the <a href="md_viewer.html">Finjin viewer</a>.
  * To load a file named *file.scene-fstd* into Finjin viewer: 
    * If the file is located within the viewer's *app* subdirectory: *finjin-viewer -file file.scene-fstd*
    * If the file is located outside the viewer's *app* subdirectory: *finjin-viewer -file /absolute/path/to/file.scene-fstd*

\section engine_asset_directory_structure Asset Directory Structure

Finjin asset files are organized beneath a root directory, and a number of specifically named subdirectories. 

An example asset directory:
```
root
  meshes
  morphanims
  nodeanims
  poseanims
  prefabs
  scenes
  skeletons  
  textures
```

The subdirectory names correspond to the entries in Finjin::Engine::AssetClass.

By default, an application has two asset directory roots: 
1. *engine* - Reserved for engine-provided asset files.
2. *app* - Application-specific asset files. This is a suitable location for exported files. Subdirectories will be created with their default names.

\subsection engine_asset_directory_naming Naming Asset Subdirectories
In order to support various platforms and configurations, it is possible to name subdirectories in a way that causes an asset in one subdirectory to be selected instead of one with the same name in another directory. 

For example:
```
app
  settings-d3d12
    gpu-context-static-mesh-renderer-buffer-formats.cfg
  settings-metal
    gpu-context-static-mesh-renderer-buffer-formats.cfg
  settings-vulkan
    gpu-context-static-mesh-renderer-buffer-formats.cfg
```

In the above scenario, *gpu-context-static-mesh-renderer-buffer-formats.cfg* will be read from the *settings-d3d12* subdirectory when the Direct3D12 version of the application is being run. A more detailed example follows.

```
app
  settings-win32-d3d12
    gpu-context-static-mesh-renderer-buffer-formats.cfg
  settings-uwp-d3d12
    gpu-context-static-mesh-renderer-buffer-formats.cfg
```

In the above scenario, *gpu-context-static-mesh-renderer-buffer-formats.cfg* will be read from the *settings-win32-d3d12* subdirectory when the Win32 / Direct3D12 version of the application is being run, and the *settings-uwp-d3d12* subdirectory when the UWP / Direct3D12 version is being run.

Note that the additional asset subdirectory components must be in the correct order, and must be separate by the '-' character. That means *settings-win32-d3d12* will work, but *shaders-d3d12-win32* will not.

\subsection engine_asset_directory_components Asset Subdirectory Components

| Description                             | Subdirectory String                                                                                                                                                                           | Examples                                                                                              | Special Notes                                                                                                                                                                                                                                                          |
| :-------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Asset class directory name              | inputbindings, inputdevices, materials, meshes, morphanims, nodeanims, poseanims, prefabs, scenes, settings, shaders, skeletons, skeletonanims, sounds, stringtables, textures, userdatatypes |                                                                                                       | This component is required.                                                                                                                                                                                                                                            |
| Language                                | (language code)                                                                                                                                                                               | en                                                                                                    |                                                                                                                                                                                                                                                                        |
| Country / region                        | (country code)                                                                                                                                                                                | en_us, en_gb                                                                                          | Language and country / region are specified together as *language_country* and must both be lower case. See [Language / country codes (External link)](https://docs.oracle.com/cd/E13214_01/wli/docs92/xref/xqisocodes.html) for a list of language and country codes. |
| CPU architecture                        | cpu_x86, cpu_x64, cpu_arm32, cpu_arm64                                                                                                                                                        |                                                                                                   |                                                                                                                                                                                                                                                                            |
| CPU byte order                          | bigendian, littleendian                                                                                                                                                                       |                                                                                                       |                                                                                                                                                                                                                                                                        |
| Operating system                        | windows, macos, ios, tvos, linux, android                                                                                                                                                     |                                                                                                       |                                                                                                                                                                                                                                                                        |
| Operating system version                | v_(major)_(minor) or v_(number)                                                                                                                                                               | v_1_0, v_14                                                                                           | The *major*, *minor*, *number* strings are specific to the operating system.                                                                                                                                                                                           |
| Application platform                    | win32, uwp                                                                                                                                                                                    |                                                                                                       |                                                                                                                                                                                                                                                                        |
| GPU system                              | d3d12, vulkan, metal                                                                                                                                                                          |                                                                                                       |                                                                                                                                                                                                                                                                        |
| GPU feature level                       | gpufeature_(level)                                                                                                                                                                            | (Direct3D 12) gpufeature_10_1                                                                         | The *level* string is specific to the GPU system.                                                                                                                                                                                                                      |
| GPU shader model                        | gpusm_(version)                                                                                                                                                                               | (Direct3D 12) gpusm_5_1, gpusm_nv_5_1                                                                 | The *version* string is specific to the GPU system.                                                                                                                                                                                                                    |
| GPU preferred texture format            | astc, bc, etc2                                                                                                                                                                                |                                                                                                       | A texture format is not the same as a file format. Texture file formats are capable of storing many different texture formats.                                                                                                                                         |
| Sound system                            | xaudio2, avaudioengine, opensles, openal                                                                                                                                                      |                                                                                                       |                                                                                                                                                                                                                                                                        |
| Input device type                       | gamecontroller, keyboard, mouse, touchscreen, accelerometer                                                                                                                                   |                                                                                                       |                                                                                                                                                                                                                                                                        |
| Input system                            | win32input, uwpinput, iosinput, macosinput, linuxinput                                                                                                                                        |                                                                                                       |                                                                                                                                                                                                                                                                        |
| Input API                               | xinput, dinput, gcinput                                                                                                                                                                       |                                                                                                       |                                                                                                                                                                                                                                                                        |
| Input device descriptor                 | inputdevice_(product descriptor)                                                                                                                                                              | (DirectInput) inputdevice_4c05c405_0000_0000_0000_504944564944, (Android) inputdevice_vid2341_pid1000 | The *product descriptor* string is specific to the input system.                                                                                                                                                                                                       |
| Device model                            | device_(model)                                                                                                                                                                                | device_nexus6, device_ipad                                                                            |                                                                                                                                                                                                                                                                        |
        

\section engine_tested_hardware_software Tested Hardware / Software

| Operating System / Platform      | Class                    | Make / Name                                        | Model / Version                 | Special Notes                                                              |
| :------------------------------: | :----------------------: | :------------------------------------------------: | :-----------------------------: | :------------------------------------------------------------------------: |
| Android                          | Input device             | Touch screen                                       |                                 |                                                                            |
| Android                          | Input device             | Accelerometer                                      |                                 |                                                                            |
| Android                          | Input device             | Standard keyboard                                  |                                 |                                                                            |
| Android                          | Input device             | Standard mouse                                     |                                 |                                                                            |
| Android                          | Input device             | Xbox 360 controller                                |                                 |                                                                            |
| Android                          | Input device             | NVidia controller                                  |                                 |                                                                            |
| Android                          | Input device             | Playstation 4 controller                           |                                 |                                                                            |
| Android                          | Input device             | Playstation 3 controller                           |                                 |                                                                            |
| Android                          | Input device             | Mayflash Wii Classic controller to PC USB adapter  |                                 |                                                                            |
| Android                          | Input device             | Logitech Dual Action controller                    |                                 |                                                                            |
| Android                          | Console                  | NVidia Shield TV                                   |                                 |                                                                            |
| Android                          | Tablet                   | NVidia Shield Tablet                               |                                 |                                                                            |
| iOS                              | Input device             | Touch screen                                       |                                 |                                                                            |
| iOS                              | Input device             | SteelSeries Nimbus Wireless Gaming Controller      |                                 | Any MFi game controller should work                                        |
| iOS                              | Smartphone               | iPhone                                             | iPhone 6+                       |                                                                            |
| Linux                            | Input device             | Standard keyboard                                  |                                 |                                                                            |
| Linux                            | Input device             | Standard mouse                                     |                                 |                                                                            |
| Linux                            | Input device             | Xbox 360 controller                                |                                 |                                                                            |
| Linux                            | Input device             | Logitech Dual Action controller                    |                                 |                                                                            |
| Linux                            | Input device             | Playstation 3 controller                           |                                 |                                                                            |
| Linux                            | Input device             | Mayflash Wii Classic controller to PC USB adapter  |                                 |                                                                            |
| Linux                            | Desktop                  | Ubuntu                                             | 15.10                           | Default Unity desktop                                                      |
| Linux                            | GPU                      | NVidia GeForce                                     | GTX 660                         | Driver version 367.18                                                      |
| macOS                            | Input device             | Standard keyboard                                  |                                 |                                                                            |
| macOS                            | Input device             | Standard mouse                                     |                                 |                                                                            |
| macOS                            | Input device             | SteelSeries Nimbus Wireless Gaming Controller      |                                 | Any MFi game controller should work                                        |
| macOS                            | Laptop computer          | Macbook Pro                                        | 13-inch, 2015                   |                                                                            |
| tvOS                             | Input device             | Remote controller                                  |                                 |                                                                            |
| tvOS                             | Input device             | SteelSeries Nimbus Wireless Gaming Controller      |                                 | Any MFi game controller should work                                        |
| tvOS                             | Console                  | Apple TV                                           | 4th Generation                  |                                                                            |
| Windows 7, 8.1                   | Input device             | Standard keyboard                                  |                                 |                                                                            |
| Windows 7, 8.1                   | Input device             | Standard mouse                                     |                                 |                                                                            |
| Windows 7, 8.1                   | Input device             | Xbox 360 controller                                |                                 | Any XInput game controller should work                                     |
| Windows 7, 8.1                   | Input device             | Playstation 4 controller                           |                                 | Uses DirectInput                                                           |
| Windows 7, 8.1                   | Input device             | Playstation 3 controller                           |                                 | Uses DirectInput. Official controller doesn't work but unofficial ones do. |
| Windows 7, 8.1                   | Input device             | Logitech Dual Action controller                    |                                 | Uses DirectInput                                                           |
| Windows 7, 8.1                   | Input device             | Mayflash Wii Classic controller to PC USB adapter  |                                 | Uses DirectInput                                                           |
| Windows 7, 8.1                   | Input device             | Gamecube controller adapter for Wii U and PC       |                                 | Uses DirectInput                                                           |
| Windows 8.1                      | GPU                      | AMD Radeon                                         | R9 280 (HD 7950)                |                                                                            |
| Windows 10 / UWP                 | Input device             | Touch screen                                       |                                 |                                                                            |
| Windows 10 / UWP                 | Input device             | Standard keyboard                                  |                                 |                                                                            |
| Windows 10 / UWP                 | Input device             | Standard mouse                                     |                                 |                                                                            |
| Windows 10 / UWP                 | Input device             | Xbox 360 controller                                |                                 | Any XInput game controller should work                                     |
| Windows 10 / UWP                 | GPU                      | NVidia GeForce                                     | GTX 980                         |                                                                            |
| Windows 10 / Win32               | Input device             | Standard keyboard                                  |                                 |                                                                            |
| Windows 10 / Win32               | Input device             | Standard mouse                                     |                                 |                                                                            |
| Windows 10 / Win32               | Input device             | Xbox 360 controller                                |                                 | Any XInput game controller should work                                     |
| Windows 10 / Win32               | Input device             | Playstation 4 controller                           |                                 | Uses DirectInput                                                           |
| Windows 10 / Win32               | Input device             | Playstation 3 controller                           |                                 | Uses DirectInput. Official controller doesn't work but unofficial ones do. |
| Windows 10 / Win32               | Input device             | Logitech Dual Action controller                    |                                 | Uses DirectInput                                                           |
| Windows 10 / Win32               | Input device             | Gamecube controller adapter for Wii U and PC       |                                 | Uses DirectInput                                                           |
| Windows 10 / Win32               | GPU                      | NVidia GeForce                                     | GTX 980                         |                                                                            |
  
  

\section engine_license License

* https://www.mozilla.org/en-US/MPL/2.0/

	
	
\section engine_credits Credits

* Boost - [boost.org](http://www.boost.org)
```
Boost Software License - Version 1.0 - August 17th, 2003

Permission is hereby granted, free of charge, to any person or organization
obtaining a copy of the software and accompanying documentation covered by
this license (the "Software") to use, reproduce, display, distribute,
execute, and transmit the Software, and to prepare derivative works of the
Software, and to permit third-parties to whom the Software is furnished to
do so, all subject to the following:

The copyright notices in the Software and this entire statement, including
the above license grant, this restriction and the following disclaimer,
must be included in all copies of the Software, in whole or in part, and
all derivative works of the Software, unless such copies or derivative
works are solely in the form of machine-executable object code generated by
a source language processor.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT
SHALL THE COPYRIGHT HOLDERS OR ANYONE DISTRIBUTING THE SOFTWARE BE LIABLE
FOR ANY DAMAGES OR OTHER LIABILITY, WHETHER IN CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.
```

* uriparser - [uriparser.sourceforge.net](http://uriparser.sourceforge.net)
```
uriparser - RFC 3986 URI parsing library

Copyright (C) 2007, Weijia Song <songweijia@gmail.com>
Copyright (C) 2007, Sebastian Pipping <webmaster@hartwork.org>
All rights reserved.

Redistribution  and use in source and binary forms, with or without
modification,  are permitted provided that the following conditions
are met:

    * Redistributions   of  source  code  must  retain  the   above
      copyright  notice, this list of conditions and the  following
      disclaimer.

    * Redistributions  in  binary  form must  reproduce  the  above
      copyright  notice, this list of conditions and the  following
      disclaimer   in  the  documentation  and/or  other  materials
      provided with the distribution.

    * Neither  the name of the <ORGANIZATION> nor the names of  its
      contributors  may  be  used to endorse  or  promote  products
      derived  from  this software without specific  prior  written
      permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS  IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT  NOT
LIMITED  TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND  FITNESS
FOR  A  PARTICULAR  PURPOSE ARE DISCLAIMED. IN NO EVENT  SHALL  THE
COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
INCIDENTAL,    SPECIAL,   EXEMPLARY,   OR   CONSEQUENTIAL   DAMAGES
(INCLUDING,  BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES;  LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
STRICT  LIABILITY,  OR  TORT (INCLUDING  NEGLIGENCE  OR  OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED
OF THE POSSIBILITY OF SUCH DAMAGE.
```

* Boost.Nowide - [cppcms.com/files/nowide](http://cppcms.com/files/nowide/html)
```
Boost Software License - Version 1.0 - August 17th, 2003
Permission is hereby granted, free of charge, to any person or organization
obtaining a copy of the software and accompanying documentation covered by
this license (the "Software") to use, reproduce, display, distribute,
execute, and transmit the Software, and to prepare derivative works of the
Software, and to permit third-parties to whom the Software is furnished to
do so, all subject to the following:

The copyright notices in the Software and this entire statement, including
the above license grant, this restriction and the following disclaimer,
must be included in all copies of the Software, in whole or in part, and
all derivative works of the Software, unless such copies or derivative
works are solely in the form of machine-executable object code generated by
a source language processor.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT
SHALL THE COPYRIGHT HOLDERS OR ANYONE DISTRIBUTING THE SOFTWARE BE LIABLE
FOR ANY DAMAGES OR OTHER LIABILITY, WHETHER IN CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.
```

* zlib - [zlib.net](http://www.zlib.net)
```
zlib.h -- interface of the 'zlib' general purpose compression library
version 1.2.11, January 15th, 2017

Copyright (C) 1995-2017 Jean-loup Gailly and Mark Adler

This software is provided 'as-is', without any express or implied
warranty.  In no event will the authors be held liable for any damages
arising from the use of this software.

Permission is granted to anyone to use this software for any purpose,
including commercial applications, and to alter it and redistribute it
freely, subject to the following restrictions:

1. The origin of this software must not be misrepresented; you must not
   claim that you wrote the original software. If you use this software
   in a product, an acknowledgment in the product documentation would be
   appreciated but is not required.
2. Altered source versions must be plainly marked as such, and must not be
   misrepresented as being the original software.
3. This notice may not be removed or altered from any source distribution.

Jean-loup Gailly        Mark Adler
jloup@gzip.org          madler@alumni.caltech.edu
```

* zziplib - [zziplib.sourceforge.net](http://zziplib.sourceforge.net)
```
Mozilla Public License Version 2.0
==================================

Full license at https://www.mozilla.org/en-US/MPL/2.0/
```

* RapidJSON - [github.com/miloyip/rapidjson](https://github.com/miloyip/rapidjson)
```
Tencent is pleased to support the open source community by making RapidJSON available. 
 
Copyright (C) 2015 THL A29 Limited, a Tencent company, and Milo Yip.  All rights reserved.

If you have downloaded a copy of the RapidJSON binary from Tencent, please note that the RapidJSON binary is licensed under the MIT License.
If you have downloaded a copy of the RapidJSON source code from Tencent, please note that RapidJSON source code is licensed under the MIT License, except for the third-party components listed below which are subject to different license terms.  Your integration of RapidJSON into your own projects may require compliance with the MIT License, as well as the other licenses applicable to the third-party components included within RapidJSON. To avoid the problematic JSON license in your own projects, it's sufficient to exclude the bin/jsonchecker/ directory, as it's the only code under the JSON license.
A copy of the MIT License is included in this file.

Other dependencies and licenses:

Open Source Software Licensed Under the BSD License:
--------------------------------------------------------------------

The msinttypes r29 
Copyright (c) 2006-2013 Alexander Chemeris 
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer. 
* Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
* Neither the name of  copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS'' AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS AND CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

Open Source Software Licensed Under the JSON License:
--------------------------------------------------------------------

json.org 
Copyright (c) 2002 JSON.org
All Rights Reserved.

JSON_checker
Copyright (c) 2002 JSON.org
All Rights Reserved.

	
Terms of the JSON License:
---------------------------------------------------

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

The Software shall be used for Good, not Evil.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


Terms of the MIT License:
--------------------------------------------------------------------

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

* Eigen - [eigen.tuxfamily.org](http://eigen.tuxfamily.org/index.php)
```
Mozilla Public License Version 2.0
==================================

Full license at https://www.mozilla.org/en-US/MPL/2.0/
```

* libpng - [libpng.org](http://www.libpng.org/pub/png/libpng.html)
```

This copy of the libpng notices is provided for your convenience.  In case of
any discrepancy between this copy and the notices in the file png.h that is
included in the libpng distribution, the latter shall prevail.

COPYRIGHT NOTICE, DISCLAIMER, and LICENSE:

If you modify libpng you may insert additional notices immediately following
this sentence.

This code is released under the libpng license.

libpng versions 1.0.7, July 1, 2000 through 1.6.29, March 16, 2017 are
Copyright (c) 2000-2002, 2004, 2006-2017 Glenn Randers-Pehrson, are
derived from libpng-1.0.6, and are distributed according to the same
disclaimer and license as libpng-1.0.6 with the following individuals
added to the list of Contributing Authors:

   Simon-Pierre Cadieux
   Eric S. Raymond
   Mans Rullgard
   Cosmin Truta
   Gilles Vollant
   James Yu
   Mandar Sahastrabuddhe
   Google Inc.
   Vadim Barkov

and with the following additions to the disclaimer:

   There is no warranty against interference with your enjoyment of the
   library or against infringement.  There is no warranty that our
   efforts or the library will fulfill any of your particular purposes
   or needs.  This library is provided with all faults, and the entire
   risk of satisfactory quality, performance, accuracy, and effort is with
   the user.

Some files in the "contrib" directory and some configure-generated
files that are distributed with libpng have other copyright owners and
are released under other open source licenses.

libpng versions 0.97, January 1998, through 1.0.6, March 20, 2000, are
Copyright (c) 1998-2000 Glenn Randers-Pehrson, are derived from
libpng-0.96, and are distributed according to the same disclaimer and
license as libpng-0.96, with the following individuals added to the list
of Contributing Authors:

   Tom Lane
   Glenn Randers-Pehrson
   Willem van Schaik

libpng versions 0.89, June 1996, through 0.96, May 1997, are
Copyright (c) 1996-1997 Andreas Dilger, are derived from libpng-0.88,
and are distributed according to the same disclaimer and license as
libpng-0.88, with the following individuals added to the list of
Contributing Authors:

   John Bowler
   Kevin Bracey
   Sam Bushell
   Magnus Holmgren
   Greg Roelofs
   Tom Tanner

Some files in the "scripts" directory have other copyright owners
but are released under this license.

libpng versions 0.5, May 1995, through 0.88, January 1996, are
Copyright (c) 1995-1996 Guy Eric Schalnat, Group 42, Inc.

For the purposes of this copyright and license, "Contributing Authors"
is defined as the following set of individuals:

   Andreas Dilger
   Dave Martindale
   Guy Eric Schalnat
   Paul Schmidt
   Tim Wegner

The PNG Reference Library is supplied "AS IS".  The Contributing Authors
and Group 42, Inc. disclaim all warranties, expressed or implied,
including, without limitation, the warranties of merchantability and of
fitness for any purpose.  The Contributing Authors and Group 42, Inc.
assume no liability for direct, indirect, incidental, special, exemplary,
or consequential damages, which may result from the use of the PNG
Reference Library, even if advised of the possibility of such damage.

Permission is hereby granted to use, copy, modify, and distribute this
source code, or portions hereof, for any purpose, without fee, subject
to the following restrictions:

  1. The origin of this source code must not be misrepresented.

  2. Altered versions must be plainly marked as such and must not
     be misrepresented as being the original source.

  3. This Copyright notice may not be removed or altered from any
     source or altered source distribution.

The Contributing Authors and Group 42, Inc. specifically permit, without
fee, and encourage the use of this source code as a component to
supporting the PNG file format in commercial products.  If you use this
source code in a product, acknowledgment is not required but would be
appreciated.

END OF COPYRIGHT NOTICE, DISCLAIMER, and LICENSE.

TRADEMARK:

The name "libpng" has not been registered by the Copyright owner
as a trademark in any jurisdiction.  However, because libpng has
been distributed and maintained world-wide, continually since 1995,
the Copyright owner claims "common-law trademark protection" in any
jurisdiction where common-law trademark is recognized.

OSI CERTIFICATION:

Libpng is OSI Certified Open Source Software.  OSI Certified Open Source is
a certification mark of the Open Source Initiative. OSI has not addressed
the additional disclaimers inserted at version 1.0.7.

EXPORT CONTROL:

The Copyright owner believes that the Export Control Classification
Number (ECCN) for libpng is EAR99, which means not subject to export
controls or International Traffic in Arms Regulations (ITAR) because
it is open source, publicly available software, that does not contain
any encryption software.  See the EAR, paragraphs 734.3(b)(3) and
734.7(b).

Glenn Randers-Pehrson
glennrp at users.sourceforge.net
March 16, 2017
```

* TinyXml-2 - [grinninglizard.com](http://www.grinninglizard.com/tinyxml)
```
Original code by Lee Thomason (www.grinninglizard.com)

This software is provided 'as-is', without any express or implied
warranty. In no event will the authors be held liable for any
damages arising from the use of this software.

Permission is granted to anyone to use this software for any
purpose, including commercial applications, and to alter it and
redistribute it freely, subject to the following restrictions:

1. The origin of this software must not be misrepresented; you must
not claim that you wrote the original software. If you use this
software in a product, an acknowledgment in the product documentation
would be appreciated but is not required.


2. Altered source versions must be plainly marked as such, and
must not be misrepresented as being the original software.

3. This notice may not be removed or altered from any source
distribution.
```

* xxHash - [xxhash.com](http://www.xxhash.com)
```
xxHash Library
Copyright (c) 2012-2014, Yann Collet
All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice, this
  list of conditions and the following disclaimer in the documentation and/or
  other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

* Bullet Physics Library - [bulletphysics.org](http://bulletphysics.org/)
```
The files in are licensed under the zlib license, except for the files under 'bullet3/Extras' and 'bullet3/examples/ThirdPartyLibs'.

Bullet Continuous Collision Detection and Physics Library
http://bulletphysics.org

This software is provided 'as-is', without any express or implied warranty.
In no event will the authors be held liable for any damages arising from the use of this software.
Permission is granted to anyone to use this software for any purpose,
including commercial applications, and to alter it and redistribute it freely,
subject to the following restrictions:

1. The origin of this software must not be misrepresented; you must not claim that you wrote the original software. If you use this software in a product, an acknowledgment in the product documentation would be appreciated but is not required.
2. Altered source versions must be plainly marked as such, and must not be misrepresented as being the original software.
3. This notice may not be removed or altered from any source distribution.
```

* Recast Navigation - [github.com/recastnavigation](https://github.com/recastnavigation)
```
Copyright (c) 2009 Mikko Mononen memon@inside.org

This software is provided 'as-is', without any express or implied
warranty.  In no event will the authors be held liable for any damages
arising from the use of this software.

Permission is granted to anyone to use this software for any purpose,
including commercial applications, and to alter it and redistribute it
freely, subject to the following restrictions:

1. The origin of this software must not be misrepresented; you must not
claim that you wrote the original software. If you use this software
in a product, an acknowledgment in the product documentation would be
appreciated but is not required.
2. Altered source versions must be plainly marked as such, and must not be
misrepresented as being the original software.
3. This notice may not be removed or altered from any source distribution.
```

* imgui - [github.com/ocornut/imgui](https://github.com/ocornut/imgui)
```
The MIT License (MIT)

Copyright (c) 2014-2015 Omar Cornut and ImGui contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
