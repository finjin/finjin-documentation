## Finjin Exporter

```
This documentation is preliminary.
```

\section exporter_about About
The Finjin exporter plug-ins for 3DS Max and Maya generate 3D assets for use with the Finjin engine.



\section exporter_features Features
* Supports 3DS Max on Windows, and Maya on Windows and MacOS.
* Includes installer applications.
* Dialogs for editing global, scene, and object settings.
* Custom user data type system.
* And more...



\section exporter_supported_modellers Supported 3D Applications / Platforms

| Application                      | Platform                       | Runtime Requirements                                                                                                                                                                                                                                                           | Development Requirements                                                       |
| :------------------------------: | :----------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------: |
| 3DS Max 2017 (Coming soon)       | Windows 7 (64-bit) and higher  | [DirectX runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?id=48145)                                   | Visual Studio 2015                                                             |
| 3DS Max 2016 / 2015              | Windows 7 (64-bit) and higher  | [DirectX runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?id=48145) (for installer)                   | Visual Studio 2012 Update 4 (for exporter), Visual Studio 2015 (for installer) |
| Maya 2017 (Coming soon)          | Windows 7 (64-bit) and higher  | [DirectX runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?id=48145)                                   | Visual Studio 2015                                                             |
| Maya 2016 / 2015                 | Windows 7 (64-bit) and higher  | [DirectX runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=35) (for exporter), [Visual Studio 2015 runtimes (External link)](https://www.microsoft.com/en-us/download/details.aspx?id=48145) (for installer)                   | Visual Studio 2012 Update 4 (for exporter), Visual Studio 2015 (for installer) |
| Maya 2017 (Coming soon)          | MacOS X                        |                                                                                                                                                                                                                                                                                | XCode                                                                          |
| Maya 2016 / 2015                 | MacOS X                        |                                                                                                                                                                                                                                                                                | XCode                                                                          |

 
	
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

* wxWidgets - [wxwidgets.org](http://www.wxwidgets.org)
```
wxWindows Library Licence, Version 3.1
              ======================================

Copyright (c) 1998-2005 Julian Smart, Robert Roebling et al

Everyone is permitted to copy and distribute verbatim copies
of this licence document, but changing it is not allowed.

                     WXWINDOWS LIBRARY LICENCE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

This library is free software; you can redistribute it and/or modify it
under the terms of the GNU Library General Public Licence as published by
the Free Software Foundation; either version 2 of the Licence, or (at your
option) any later version.

This library is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Library General Public
Licence for more details.

You should have received a copy of the GNU Library General Public Licence
along with this software, usually in a file named COPYING.LIB.  If not,
write to the Free Software Foundation, Inc., 51 Franklin Street, Fifth
Floor, Boston, MA 02110-1301 USA.

EXCEPTION NOTICE

1. As a special exception, the copyright holders of this library give
permission for additional uses of the text contained in this release of the
library as licenced under the wxWindows Library Licence, applying either
version 3.1 of the Licence, or (at your option) any later version of the
Licence as published by the copyright holders of version 3.1 of the Licence
document.

2. The exception is that you may use, copy, link, modify and distribute
under your own terms, binary object code versions of works based on the
Library.

3. If you copy code from files distributed under the terms of the GNU
General Public Licence or the GNU Library General Public Licence into a
copy of this library, as this licence permits, the exception does not apply
to the code that you add in this way.  To avoid misleading anyone as to the
status of such modified files, you must delete this exception notice from
such code and/or adjust the licensing conditions notice accordingly.

4. If you write modifications of your own for this library, it is your
choice whether to permit this exception to apply to your modifications.  If
you do not wish that, you must delete the exception notice from such code
and/or adjust the licensing conditions notice accordingly.
```
