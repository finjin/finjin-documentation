## Finjin Engine

```
This documentation is preliminary.
```

\section engine_about About

The Finjin engine provides the core functionality for applications.

\section engine_features Features
* Creates application windows.
* Implements the main application loop.
* Provides a multithreaded job system for distributing work across multiple cores.
* Provides readers for streaming in scene data.
* And more...

\section engine_supported_platforms Supported Operating Systems / Platforms

| Operating System / Platform      | Graphics System | Sound System     | Input System                                        | Special Notes                                                 |
| :------------------------------: | :-------------: | :--------------: | :-------------------------------------------------: | ------------------------------------------------------------- |
| Android 6+ (Coming soon)         | Vulkan          | OpenSL ES        | Standard window input                               | Multiple windows not available.                               |
| iOS 10+ (Coming soon)            | Metal           | AVAudioEngine    | Standard window input and Game Controller framework | Multiple windows not available.                               |
| Linux (Coming soon)              | Vulkan          | OpenAL           | Standard window input                               |                                                               |
| macOS 10+ (Coming soon)          | Metal           | AVAudioEngine    | Standard window input and Game Controller framework |                                                               |
| tvOS 10+ (Coming soon)           | Metal           | AVAudioEngine    | Standard window input and Game Controller framework | Multiple windows not available.                               |
| Windows 7, 8.1 (Coming soon)     | Vulkan          | XAudio2          | XInput and DirectInput                              |                                                               |
| Windows 10 / UWP                 | D3D12           | XAudio2          | Standard window input and XInput                    | Multiple windows not available.                               |
| Windows 10 / Win32               | D3D12 or Vulkan | XAudio2          | XInput and DirectInput                              | D3D12 and Vulkan versions are separate executables.           |

\section engine_dev_target_tools Development Target Tools

* All targets:
  * Python 3.x - Some utilities are written in Python.

| Target                           | Development Platform | Development Environment            | Additional Software                                                               | Special Notes                                                 |
| :------------------------------: | :------------------: | :--------------------------------: | :-------------------------------------------------------------------------------: | ------------------------------------------------------------- |
| Android                          | Windows              | Visual Studio 2015 with Update 3   | [NVidia CodeWorks for Android] (https://developer.nvidia.com/gameworksdownload)   | Applications must be run on target device, not the simulator. |
| iOS / macOS / tvOS               | macOS                | XCode 8                            |                                                                                   | Applications must be run on target device, not the simulator. |
| Linux                            | Linux                | NetBeans 8.1                       |                                                                                   |                                                               |
| Windows / Win32                  | Windows 7 and higher | Visual Studio 2015 with Update 3   |                                                                                   |                                                               |
| Windows / UWP                    | Windows 10           | Visual Studio 2015 with Update 3   |                                                                                   | Applications must be run on target device, not the simulator. |


	
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

| Name                                                               | Extension | Encoding     | Line Ending   | Reader Memory Usage                                                | Hand-Written Files Acceptable     | Best Use                                                              | Related Classes                                                                                                                                          | Special Notes                                                                                                                                                                                                                  |
| :----------------------------------------------------------------: | :-------: | :----------: | :-----------: | :----------------------------------------------------------------: | :-------------------------------: | :-------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Finjin Streaming Text Document                                     | .fstd     | Text / UTF-8 | \\n           | One data line - Up to *max-bytes-per-line*, as defined in the file | No - Specific formatting required | Most assets - development and archiving                               | Finjin::Common::TextDataChunkReader, Finjin::Common::TextDataChunkWriter                                                                                 | 1)Ensure your source control system doesn't alter line endings for this file type. 2)A data line may contain multiple newline characters.                                                                                      |
| Finjin Streaming Binary Document                                   | .fsbd     | Binary       | (none)        | One data line - Up to *max-bytes-per-line*, as defined in the file | No                                | Most assets - production                                              | Finjin::Common::BinaryDataChunkReader, Finjin::Common::BinaryDataChunkWriter                                                                             | 1)Ensure your source control system treats this file type as a binary file.                                                                                                                                                    |
| <a href="#engine_extended_config_file_format">Extended Config</a>  | .cfg      | Text / UTF-8 | \\r\\n or \\n | Entire file                                                        | Yes                               | Configuration files that can be modified by hand                      | Finjin::Common::ConfigDataChunkReader, Finjin::Common::ConfigDataChunkWriter, Finjin::Common::ConfigDocumentReader, Finjin::Common::ConfigDocumentWriter | 1)The writer writes \\n, but the reader reads \\r\\n or \\n.                                                                                                                                                                   |
| JSON                                                               | .json     | Text / UTF-8 | \\r\\n or \\n | One data line - Up to the size of the longest line in the file     | No - Specific formatting required | Assets that can be read by a standard JSON parser outside the engine  | Finjin::Common::JsonDataChunkReader, Finjin::Common::JsonDataChunkWriter                                                                                 | 1)The writer writes \\n, but the reader reads \\r\\n or \\n. 2)JsonDataChunkWriter or the Finjin exporters must be used to create these files (not an external JSON writer) due to specific formatting requirements.           |
| Texture                                                            | .texture  | Binary       | (none)        | Entire file                                                        | No                                | Textures                                                              | Finjin::Common::WrappedFileReader, Finjin::Common::WrappedFileWriter                                                                                     | 1)This file contains an embedded image file. The image format must be supported to load successfully. 2)WrappedFileWriter, wrap_file.py, or the Finjin exporters must be used to create these files.                           |
| Sound                                                              | .sound    | Binary       | (none)        | Entire file                                                        | No                                | Sounds                                                              | Finjin::Common::WrappedFileReader, Finjin::Common::WrappedFileWriter                                                                                       | 1)This file contains an embedded sound file. The sound format must be supported to load successfully. 2)WrappedFileWriter, wrap_file.py, or the Finjin exporters must be used to create these files.                           |

\subsection engine_external_file_formats External File Formats

| Name                                                               | Extension | Encoding     | Line Ending   | Reader Memory Usage                                                | Hand-Written Files Acceptable     | Best Use                                                              | Related Classes                                                                                                                                          | Special Notes                                                                                                                                                                                                                  |
| :----------------------------------------------------------------: | :-------: | :----------: | :-----------: | :----------------------------------------------------------------: | :-------------------------------: | :-------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DDS                                                                | .dds      | Binary       | (none)        | Entire file                                                        | No                                | Textures                                                              | Finjin::Engine::DDSReader                                                                                                                                | This file type is supported by the D3D12 graphics system.                                                                                                                                                                      |
| PNG                                                                | .png      | Binary       | (none)        | Entire file                                                        | No                                | Textures                                                              | Finjin::Common::PNGReader                                                                                                                                |                                                                                                                                                                                                                                |
| WAV                                                                | .wav      | Binary       | (none)        | Entire file                                                        | No                                | Sound effects                                                         | Finjin::Engine::WAVReader                                                                                                                                |                                                                                                                                                                                                                                |

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
  shaders-d3d12
    some-shaders.shader
  shaders-metal
    some-shaders.shader
  shaders-vulkan
    some-shaders.shader
```

In the above scenario, *some-shaders.shader* will be read from the *shaders-d3d12* subdirectory when the Direct3D12 version of the application is being run. A more detailed example follows.

```
app
  shaders-win32-d3d12
    some-shaders.shader
  shaders-uwp-d3d12
    some-shaders.shader
```

In the above scenario, *some-shaders.shader* will be read from the *shaders-win32-d3d12* subdirectory when the Win32 / Direct3D12 version of the application is being run, and the *shaders-uwp-d3d12* subdirectory when the UWP / Direct3D12 version is being run.

Note that the additional asset subdirectory components must be in the correct order, and must be separate by the '-' character. That means *shaders-win32-d3d12* will work, but *shaders+d3d12+win32* will not.

\subsection engine_asset_directory_components Asset Subdirectory Components

| Description                             | Subdirectory String                                                                                                                                                                           | Examples                                                                                              | Special Notes                                                              |
| :-------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------: |
| Asset class directory name              | inputbindings, inputdevices, materials, meshes, morphanims, nodeanims, poseanims, prefabs, scenes, settings, shaders, skeletons, skeletonanims, sounds, stringtables, textures, userdatatypes |                                                                                                       | This component is required.                                                |
| Language                                | (language code)                                                                                                                                                                               | en                                                                                                    |                                                                            |
| Country / region                        | (country code)                                                                                                                                                                                | en_us, en_gb                                                                                          | Language and country / region are specified together as *language_country* |
| CPU architecture                        | cpu_(arch)                                                                                                                                                                                    | cpu_x64, cpu_arm64                                                                                    |                                                                            |
| CPU byte order                          | bigendian, littleendian                                                                                                                                                                       |                                                                                                       |                                                                            |
| Operating system                        | windows, macos, ios, tvos, linux, android                                                                                                                                                     |                                                                                                       |                                                                            |
| Operating system version                | v_(major)_(minor) or v_(major)                                                                                                                                                                | v_1_0, v_14                                                                                           | The *major* and *minor* strings are specific to the operating system.      |
| Application platform                    | win32, uwp                                                                                                                                                                                    |                                                                                                       |                                                                            |
| GPU system                              | d3d12, vulkan, metal                                                                                                                                                                          |                                                                                                       |                                                                            |
| GPU feature level                       | gpufeature_(level)                                                                                                                                                                            | (Direct3D 12) gpufeature_10_1                                                                         | The *level* string is specific to the GPU system.                          |
| GPU shader model                        | gpusm_(version)                                                                                                                                                                               | (Direct3D 12) gpusm_5_1, gpusm_nv_5_1                                                                 | The *version* string is specific to the GPU system.                        |
| Sound system                            | xaudio2, avaudioengine, opensles, openal                                                                                                                                                      |                                                                                                       |                                                                            |
| Input device type                       | gamecontroller, keyboard, mouse, touchscreen, accelerometer                                                                                                                                   |                                                                                                       |                                                                            |
| Input system                            | win32input, uwpinput, iosinput, macosinput, linuxinput                                                                                                                                        |                                                                                                       |                                                                            |
| Input API                               | xinput, dinput, gcinput                                                                                                                                                                       |                                                                                                       |                                                                            |
| Input device descriptor                 | inputdevice_(product descriptor)                                                                                                                                                              | (DirectInput) inputdevice_4c05c405_0000_0000_0000_504944564944, (Android) inputdevice_vid2341_pid1000 | The *product descriptor* string is specific to the input system.           |
| Device model                            | device_(model)                                                                                                                                                                                | device_nexus6, device_ipad                                                                            |                                                                            |
        

\section engine_tested_hardware_software Tested Hardware / Software

| Operating System / Platform      | Class                    | Make / Name                                        | Model / Version                 | Special Notes                                                              |
| :------------------------------: | :----------------------: | :------------------------------------------------: | :-----------------------------: | -------------------------------------------------------------------------- |
| Android                          | Input device             | Touch screen                                       |                                 |                                                                            |
| Android                          | Input device             | Accelerometer                                      |                                 |                                                                            |
| Android                          | Input device             | Standard keyboard                                  |                                 |                                                                            |
| Android                          | Input device             | Standard mouse                                     |                                 |                                                                            |
| Android                          | Input device             | Xbox 360 controller                                |                                 |                                                                            |
| Android                          | Input device             | NVidia controller                                  |                                 |                                                                            |
| Android                          | Input device             | Playstation 4 controller                           |                                 |                                                                            |
| Android                          | Input device             | Playstation 3 controller                           |                                 |                                                                            |
| Android                          | Input device             | Mayflash Wii Classic controller to PC USB adapter  |                                 |                                                                            |
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

* boost - [http://www.boost.org](www.boost.org)
* uriparser - [http://uriparser.sourceforge.net](uriparser.sourceforge.net)
* nowide - [http://cppcms.com/files/nowide/html](cppcms.com/files/nowide)
* zlib - [http://www.zlib.net](zlib.net)
* zziplib - [http://zziplib.sourceforge.net](zziplib.sourceforge.net)
* rapidjson - [https://github.com/miloyip/rapidjson](github.com/miloyip/rapidjson)
* eigen - [http://eigen.tuxfamily.org/index.php](eigen.tuxfamily.org)
* libpng - [http://www.libpng.org/pub/png/libpng.html](www.libpng.org)
* tinyxml - [http://www.grinninglizard.com/tinyxml](www.grinninglizard.com)
