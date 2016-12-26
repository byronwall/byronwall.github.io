---
layout: post
category: blog
published: true
title: Fighting Ruby's Dir.tmpdir on Windows
---
## 500 Errors with tempfile

I was working recently with a PDF in [Tabula](http://tabula.technology/).  Previously, I have used Tabula to extract tables from PDFs.  It has worked great.  This time, I could not get Tabula to start processing the PDF.  Debugging the network request, gave a pointer about a temporary directory issue.

![Tabula upload error]({{site.baseurl}}/images/posts/2016-12-26_10-49-25.png)

The error message was a bit cryptic since it only referred to the directory `/tmp` and did not give any indication of the full path for this directory.  The error message also does not give a file or line number so I went to the code to guess where it was failing.

Since the issue is the AJAX request to  `upload.json`, I did a [search for that in the code](https://github.com/tabulapdf/tabula/search?utf8=%E2%9C%93&q=%22upload.json%22&type=Code).  You can see the two files that are returned are `tabula_web.rb` and `index.html`.  The latter is the front end UI, so I went to the [former file to spot the issue](https://github.com/tabulapdf/tabula/blob/92a23a1c1542cd082a3715ca847c2d1a532942df/webapp/tabula_web.rb#L178)

I had previously dug into the AJAX request to know that it was POSTing a parameter called `files` with the relevant info.  It would not have mattered because both code paths call `is_valid_pdf` with a parameter of `file[:tempfile].path`.  This is supposed to refer to the path of the uploaded file.  In my case, it seems was not getting into the `is_valid_pdf` function.  I added a line to the top of that function which did not generate output.

Given that, it looked like there was an issue with `Tempfile` having a correct directory to output to.

Checking the [docs of Tempfile](http://ruby-doc.org/stdlib-1.9.3/libdoc/tempfile/rdoc/Tempfile.html) you can see that it uses `Dir.tmpdir` as the output directory.  This can be controlled by an evironment variable `$TMPDIR`.  Checking my environment variables, I had nothing set for this.  I forced this variable to be equal to the directory `%USERPROFILE%/AppData/Local/Temp/tmp`, which I had just created.

With this addition and a restart of Tabula, the files uploaded correctly.
