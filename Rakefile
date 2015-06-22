require 'puppetlabs_spec_helper/rake_tasks'
require 'puppet-lint/tasks/puppet-lint'
require 'metadata-json-lint/rake_task'

begin
  require 'puppet_blacksmith/rake_tasks'
rescue LoadError
end

Rake::Task[:lint].clear
PuppetLint::RakeTask.new :lint do |config|
  config.ignore_paths = ["spec/**/*.pp", "pkg/**/*.pp", "vendor/**/*.pp"]
end

PuppetSyntax.exclude_paths = ["spec/**/*", "pkg/**/*", "vender/**/*"]
PuppetSyntax.hieradata_paths = ["**/data/**/*.yaml", "hieradata/**/*.yaml", "hiera*.yaml"]

Rake::Task['beaker'].clear
task :beaker do
  puts "Placeholder to go around the fact that there are not beaker tests for this module"
end

namespace :doc do
  docs_dir = File.dirname(__FILE__) + '/doc'

  desc 'Generate documentation with the puppet strings command'
  task :generate do
    system "bundle exec puppet module install puppetlabs/strings"
    system "bundle exec puppet strings"
  end

  desc 'Clean current documentation'
  task :clean do
    FileUtils.rm_rf(Dir.glob("#{docs_dir}/*"))
  end

  desc "Run clean and generate"
  task :update => [
    :clean,
    :generate,
  ]
end
