# Versioned CV

Versioned CV is an attempt to write CVs using Markdown syntax, versioned using Git, automatically built into PDFs.

## Install

### Install GEM dependencies:

	bundle install

### Install wkhtmltopdf

I had issues with version 0.11, so I'd suggest to use 0.10.
You can download it from here: http://wkhtmltopdf.googlecode.com/files/wkhtmltopdf-OSX-0.10.0_rc2-static.tar.bz2
Then create a symlink into your /usr/local/bin so that PDFKit can access it.

## Build

To generate PDF you just need to use rake:

	rake build

Or, if you want to build and display the PDF in a single command, just use:

	rake