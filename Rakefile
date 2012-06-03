require 'yaml'

task :default => :server

desc "Clean up generated site"
task :clean do
  cleanup
end

desc "Build site with Jekyll"
task :build => :clean do
  compass
  jekyll
end

desc 'Start server with --auto'
task :server => :clean do
  compass
  jekyll('--server --auto')
end

desc "Draft a new post"
task :draft, :title do |t, args|
  require './_plugins/titlecase.rb'
  args.with_defaults(:title => 'new-post')

  title = args.title.gsub(/&/,'&amp;').titlecase
  draft("#{title}")
end

desc "Publish a Draft"
task :publish, :filename do |t, args|
  args.with_defaults(:filename => nil)
  filename = args.filename
  publish(filename)
end

desc "Deploy it"
task :deploy => :build do
  sh 'rsync -rtzh --progress _site/ clioweb@clioweb.org:/home/clioweb/clioweb.org/'
end

def cleanup
  sh 'rm -rf _site'
end

def jekyll(opts = '')
  sh 'jekyll ' + opts
end

def compass(opts = '')
  sh 'compass compile -c config.rb --force ' + opts + ' && compass watch &'
end

def draft(title)
  slug = title.downcase.gsub(/ +/,'-').gsub(/[^-\w]/,'').sub(/-+$/,'')
  filename = slug + ".md"
  mkdir_p "_drafts"
  if File.exists?("_drafts/#{filename}")
    puts "#{filename} already exists!"
    return
  end
  File.open("_drafts/#{filename}","w+") do |f|
    f.puts "---"
    f.puts "layout: post"
    f.puts "title: #{title}"
    f.puts "---"
  end
  puts "Created _drafts/#{filename}"
end

def publish(file=nil)
  unless file
    puts "Choose file:"
    @files = Dir["_drafts/*"]
    @files.each_with_index { |f,i| puts "#{i+1}: #{f}" }
    print "> "
    num = STDIN.gets
    file = @files[num.to_i - 1]
  end
  now = Time.now.strftime("%Y-%m-%d")
  mv file, "_posts/#{now}-#{File.basename(file)}"
end
