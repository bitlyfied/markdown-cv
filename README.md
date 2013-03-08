# Markdown CV

Markdown CV is an attempt to write CVs using Markdown syntax, versioned using Git, automatically built into PDFs.

**Warning: I wrote this code just for my personal use. Feel free to use it, but don't expect it to be well tested or even near to a beta version.** 

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

## Use

Put your CVs in the src folder. All files *.md are built by the rake task.
You can use the one provided as an example.

The build task is a three step process:
- convert Mardown to HTML
- render content inside a styled HTML template
- convert the HTML file to PDF using wkhtmltopdf

To tweak the style of the CV you can change the _template/base.css_ file with your own font and style.


## Enriched Markdown

Markdown CV is using Github-flavoured Markdown, and on top of that it's adding an extra feature.
You can mark blocks of content with the following syntax:

	[myblock]
	
	** Some content
	
	[/myblock]
	
The build process will replace **[myblock]** with **&lt;div class=&quot;myblock&quot;&gt;**

You can use this functionality to create asides and content formatted in a special way.

## Page breaks

Markdown has no knowledge of pages or page breaks. But you can use **page-break-** CSS to control them.

You can tackle the issue in two different ways.

- specifically request page breaks where needed (not recommended)
- define places where you don't want a page break, and let the normal flow find the right spots

For the first method, you could use custom tags in your markdown like this:

	[page-break/]

Then you just need to add some CSS like this:

	div.page-break{
		page-break-after:always;
	}

My preferred approach is to let the content flow naturally between pages, and only avoid page breaks where they shouldn't be.
The CV provided as example uses this trick.

	[block]
	
	** Some content here
		
	[/block]

Then this line of CSS ensure everything in the block will hang together:


	p, li, .block, .aside{
		page-break-inside:avoid;
	}

