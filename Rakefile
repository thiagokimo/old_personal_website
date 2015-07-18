require 'rake'
require 'time'

SOURCE = "."
CONFIG = {
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "md",
}

desc "Serve and watch the site (with post limit or drafts)"
task :watch do |t, args|
  system("LC_ALL=\"en_US.UTF-8\" jekyll serve --baseurl \"\" -w")
end

task :default => :watch

desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])

  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

  begin
    date = Time.now.strftime("%Y-%m-%d %H:%M")
    stringfied_date = Time.now.strftime('%Y-%m-%d')

  rescue => e
    puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
    exit -1
  end

  filename = File.join(CONFIG['posts'], "#{stringfied_date}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "date: #{date}"
    post.puts "summary: "
    post.puts "categories: "
    post.puts "---"
  end
end
