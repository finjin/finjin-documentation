## Finjin Exporter

```
This documentation is preliminary.
```

\section exporter_about About
The Finjin exporter plug-ins for 3DS Max and Maya generate 3D assets for use with the Finjin engine.



\section exporter_supported_modellers Supported 3D Applications / Platforms

| Application                      | Platform                       | Runtime Requirements                                                                                                                                                                                                                           | Development Requirements                                                       |
| :------------------------------: | :----------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------: |
| 3DS Max 2017 (Coming soon)       | Windows 7 (64-bit) and higher  | Updated [DirectX runtimes](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes](https://www.microsoft.com/en-us/download/details.aspx?id=48145)                           | Visual Studio 2015                                                             |
| 3DS Max 2016 / 2015              | Windows 7 (64-bit) and higher  | Updated [DirectX runtimes](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes](https://www.microsoft.com/en-us/download/details.aspx?id=48145) (for installer)           | Visual Studio 2012 Update 4 (for exporter), Visual Studio 2015 (for installer) |
| Maya 2017 (Coming soon)          | Windows 7 (64-bit) and higher  | Updated [DirectX runtimes](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes](https://www.microsoft.com/en-us/download/details.aspx?id=48145)                           | Visual Studio 2015                                                             |
| Maya 2016 / 2015                 | Windows 7 (64-bit) and higher  | Updated [DirectX runtimes](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes](https://www.microsoft.com/en-us/download/details.aspx?id=48145) (for installer)           | Visual Studio 2012 Update 4 (for exporter), Visual Studio 2015 (for installer) |

 
	
\section exporter_object_names Exported Object & Asset Names
Objects named using the \\, /, or ! character will be used to create subdirectories in the exported directory. This can be useful to group together related assets. This also applies to bitmap file names (where it's only possible to use the ! character in the file name).
* Examples
  * Bitmap / texture file names:
    * *sky!cloud.png* 
	  * The exported texture name will be *sky/cloud*. 
	  * If the *Copy Bitmaps to Export Directory* global setting is enabled and bitmaps are not being embedded in exported files, the file will be copied to *textures/sky/cloud.png*.
    * *cloud.png* (stored in current project directory or subdirectory) - 3DS Max and Maya have a notion of a project, which has a corresponding directory. Subdirectory names are incorporated into the exported texture name. 
	  * If *cloud.png* is located at (project directory)/sky/cloud.png, the exported texture name will be *sky/cloud*. 
	  * If the *Copy Bitmaps to Export Directory* global setting is enabled and bitmaps are not being embedded in exported files, the file will be copied to *textures/sky/cloud.png*.
  * Material names: 
    * *sky\\cloud* (or *sky/cloud*) 
	  * The exported material name will be *sky/cloud*. 
	  * If materials are not being embedded in exported files, the material file will be exported to *materials/sky/cloud.(file format)-material* (where 'file format' is the exported file format).
  * Mesh names: 
    * *shapes\\box* (or *shapes/box*) 
	  * The exported mesh name will be *shapes/box*. 
	  * If meshes are not being embedded in exported files, the mesh file will be exported to *meshes/shapes/box.(file format)-mesh* (where 'file format' is the exported file format).
  
  
  
\section exporter_license License
  * GNU General Public License version 3 (or later) - http://www.gnu.org/licenses

  
  
\section exporter_credits Credits
* boost - [http://www.boost.org](www.boost.org)
* uriparser - [http://uriparser.sourceforge.net](uriparser.sourceforge.net)
* nowide - [http://cppcms.com/files/nowide/html](cppcms.com/files/nowide)
* zlib - [http://www.zlib.net](zlib.net)
* zziplib - [http://zziplib.sourceforge.net](zziplib.sourceforge.net)
* rapidjson - [https://github.com/miloyip/rapidjson](github.com/miloyip/rapidjson)
* eigen - [http://eigen.tuxfamily.org/index.php](eigen.tuxfamily.org)
* libpng - [http://www.libpng.org/pub/png/libpng.html](www.libpng.org)
* tinyxml - [http://www.grinninglizard.com/tinyxml](www.grinninglizard.com)
* wxWidgets - [http://www.wxwidgets.org](www.wxwidgets.org)
