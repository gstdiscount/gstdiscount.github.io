# coding: utf-8
require 'jekyll'

# Extend string to allow for bold text.
class String
	def bold
		"\033[1m#{self}\033[0m"
	end
end

# Rake Jekyll tasks
task :build do
	puts 'Building site...'.bold
	Jekyll::Commands::Build.process(profile: true)
end

task :clean do
	puts 'Cleaning up _site...'.bold
	Jekyll::Commands::Clean.process({})
end

task :serve do
	puts 'Autoregenerating site...'.bold
	sh "bundle exec jekyll serve"
end

task :test do
	require 'html-proofer'
	sh "rm -rf ./_site"
	sh "bundle exec jekyll build"
	options = {
		:allow_hash_href => true,
		:check_favicon => false,
		:check_opengraph => true,
		:check_html => true,
		:check_img_http => true,
		:cache => { :timeframe => '15d' },
		:enforce_https => true,
		:check_external_hash => true,
		:url_ignore => [/https:\/\/web.archive.org\/web\//]
	}
	HTMLProofer.check_directory("./_site", options).run
end