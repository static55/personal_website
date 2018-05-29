---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
subheadline:  "A QT C++ app that saves encrypted notes to a CGI script written in C"
title:  "Qryptnote"
categories:
    - design
tags:
    - post format

---
<iframe src="https://player.vimeo.com/video/272304388" width="640" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/272304388">Qryptnote, a Qt app that saves encrypted notes to a cgi script.</a> from <a href="https://vimeo.com/user84877905">Stewart Rap</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

Encryption is done with libgcrypt on both the client and CGI script. The same base64.cpp/.h is used on both the client and CGI script and is copyright (C) 2013 Adam Rudd. The CGI script uses the CGIC library, a lightweight C CGI library, copyright 1996-2014 by Thomas Boutell.

I wrote 1,000 lines of C++ for the client and 500 lines of C for the CGI script.

<h3>Basic overview</h3>
<img src="/images/clientrequestssavednotes.png"><br>
<img src="/images/clientsavesnotestoserver.png"><br>

[Qryptnote client on GitHub ›](https://github.com/static55/QryptNote){: .t30 .button .radius}
[Qryptnote CGI script on GitHub ›](https://github.com/static55/QryptNote){: .t30 .button .radius}
