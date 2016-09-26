require 'rubygems'
require 'rake'
require 'yaml'
require 'time'

SOURCE = '.'
CONFIG = {
  :version => '0.3.1',
  :layouts => File.join(SOURCE, '_layouts'),
  :posts => File.join(SOURCE, '_posts'),
  :drafts => File.join(SOURCE, '_drafts'),
  :post_ext => 'md',
}

# Path configuration helper
module Jekyll
  class Path
    SOURCE = '.'
    Paths = {
      :layouts => '_layouts',
      :posts => '_posts'
    }
    
    def self.base
      SOURCE
    end

    # build a path relative to configured path settings.
    def self.build(path, opts = {})
      opts[:root] ||= SOURCE
      path = "#{opts[:root]}/#{Paths[path.to_sym]}/#{opts[:node]}".split('/')
      path.compact!
      File.__send__ :join, path
    end
  
  end #Path
end #Jekyll

desc 'Usage'
task :default do
    puts "Usage\n"
    puts "rake post title=\"title\" [date=\"date\"]\n"
    puts "rake draft [title=\"A Title\"] [tags=[tag1, tag2]]"
    puts 'rake preview [drafts=true]'
    puts "rake publish [title=\"A Title\"] [date=\"date\"]"
    puts "rake page [name=\"Page Name\"]"
end

# Usage: rake post title="A Title" [date="2012-02-09"] [tags=[tag1, tag2]]
desc "Begin a new post in #{CONFIG[:posts]}"
task :post do
  abort("rake aborted: '#{CONFIG[:posts]}' directory not found.") unless FileTest.directory?(CONFIG[:posts])
  title = ENV['title'] || 'new-post'
  tags = ENV['tags'] || ''
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
  rescue => e
    puts 'Error - date format must be YYYY-MM-DD, please check you typed it correctly!'
    exit -1
  end
  filename = File.join(CONFIG[:posts], "#{date}-#{slug}.#{CONFIG[:post_ext]}")
  if File.exist?(filename)
    abort('rake aborted!') if ask("#{filename} already exists. Do you want to overwrite?", %w(y n)) == 'n'
  end
  
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts '---'
    post.puts 'layout: post'
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts 'description: ""'
    post.puts 'category: '
    post.puts "tags: [#{tags}]"
    post.puts '---'
    post.puts ''
  end
end # task :post

# Usage: rake draft [title="A Title"] [tags=[tag1, tag2]]
# if you have no title it becomes new-post which will be the default draft to publish with the draft command
desc "Begin a new draft in #{CONFIG[:drafts]}"
task :draft do
  puts "Begin a new draft in #{CONFIG[:drafts]}"
  unless FileTest.directory?(CONFIG[:drafts])
    FileUtils.mkdir_p(CONFIG[:drafts])
  end
  
  title = ENV['title'] || 'new-post'
  tags = ENV['tags'] || '[]'
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG[:drafts], "#{slug}.#{CONFIG[:post_ext]}")
  if File.exist?(filename)  
    abort('rake aborted!') if ask("#{filename} already exists. Do you want to overwrite?", %w(y n)) == 'n'
  end

  puts "Creating new draft: #{filename}"
  open(filename, 'w') do |post|

    post.puts '---'
    post.puts 'layout: post'
    post.puts "title: \"#{title.gsub(/-/, ' ')}\""
    post.puts 'description: ""'

    post.puts 'category: '
    post.puts "tags: #{tags}"
    post.puts '---'
    post.puts ''
  end
end # task :draft

# Usage: rake publish [title="A Title"] [date="2012-02-09"]
# if you give no title it will try to publish "new post".
desc "Publish a draft in #{CONFIG[:posts]}"
task :publish do
  abort("rake aborted: '#{CONFIG[:drafts]}' directory not found.") unless FileTest.directory?(CONFIG[:drafts])

  title = ENV['title'] || 'new-post'
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG[:drafts], "#{slug}.#{CONFIG[:post_ext]}")

  puts "filename: #{filename}"


  unless File.exists?(filename)
    filename = File.join(CONFIG[:drafts], "new-post..#{CONFIG[:post_ext]}")
  end
  abort("rake aborted: no draft #{filename}' not found.") unless File.exist?(filename)
  if title == 'new-post'

    text=File.open(filename).read
    text.gsub!(/\r\n?/, "\n")
    text.each_line do |line|
      res = /^title: "([^"]+)"/.match(line)
      if res
        slug = res[1].downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
        break
      end
    end
  end

  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
  rescue => e
    puts 'Error - date format must be YYYY-MM-DD, please check you typed it correctly!'
    exit -1
  end

  put_filename = File.join(CONFIG[:posts], "#{date}-#{slug}.#{CONFIG[:post_ext]}")

  puts "Publish draft: #{filename} to #{put_filename}"

  FileUtils.cp(filename, put_filename)
  FileUtils.rm(filename)

end # task :publish

# Usage: rake page name="about.html"
# You can also specify a sub-directory path.
# If you don't specify a file extension we create an index.html at the path specified
desc 'Create a new page.'
task :page do
  name = ENV['name'] || 'new-page.md'
  filename = File.join(SOURCE, "#{name}")
  filename = File.join(filename, 'index.html') if File.extname(filename) == ''
  title = File.basename(filename, File.extname(filename)).gsub(/[\W_]/, ' ').gsub(/\b\w/){$&.upcase }
  if File.exist?(filename)
    abort('rake aborted!') if ask("#{filename} already exists. Do you want to overwrite?", %w(y n)) == 'n'
  end
  
  mkdir_p File.dirname(filename)
  puts "Creating new page: #{filename}"
  open(filename, 'w') do |post|
    post.puts '---'
    post.puts 'layout: page'
    post.puts "title: \"#{title}\""
    post.puts 'description: ""'
    post.puts '---'
    post.puts ''
  end
end # task :page

desc 'Launch preview environment'
task :preview do
  drafts = ENV['drafts'].to_s.empty? ? '' : ' --drafts'
  system "bundle exec jekyll serve --watch#{drafts}"
end # task :preview

desc 'Build site'
task :build do
  system "bundle exec jekyll build"
end # task: build



def ask(message, valid_options)
  answer = false
  if valid_options
    answer = get_stdin("#{message} #{valid_options.to_s.gsub(/"/, '').gsub(/, /, '/')} ") until valid_options.include?(answer)
  else
    answer = get_stdin(message)
  end
  answer
end

def get_stdin(message)
  print message
  STDIN.gets.chomp
end
