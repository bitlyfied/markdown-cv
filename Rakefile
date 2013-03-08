require 'rake'
require "github/markdown"
require "slim"
require "pdfkit"

task :default => ['show']

task :show => [:build] do
	sh 'open build/*.pdf'
end

task :build do
	rmtree 'build'
	mkdir_p 'build'
	
	FileList['src/*.md'].each do |src|
		html_filename = out_filename(src, 'html')
		pdf_filename = out_filename(src, 'pdf')

		to_html(src, html_filename)
		to_pdf(html_filename, pdf_filename)
	end
end

def out_filename (src, new_extension)
	'build/' + File.basename(src, '.md') + '.' + new_extension
end

def to_html (src, out)
	source = File.read(src)
	content = add_divs(GitHub::Markdown.render_gfm(source))
	output = template('base', content)

	File.open(out,'w') {|file| file.puts output}
	puts "#{src} => #{out}"
end

# replace text such as [block] with <div class="block">
def add_divs (html)
	html.gsub!(/^<p>\[(.*?)\/\]/m, '<div class="\1"></div>')
	html.gsub!(/^<p>\[\/(.*?)\]/m, '</div>')
	html.gsub!(/^<p>\[(.*?)\]/m, '<div class="\1">')
	html
end

def to_pdf (src, out)
	PDFKit.new(File.new(src), 'lowquality' => true, 'margin-left' => '1.2cm', 'margin-right' => '1.2cm', 'margin-top' => '1.2cm', 'margin-bottom' => '1.2cm').to_file(out)
	puts "#{src} => #{out}"
end

def template(tpl, content)
	Slim::Template.new("templates/" + tpl+'.slim').render(Object.new, :content => content)
end

