require 'bundler'
Bundler::GemHelper.install_tasks
require 'rspec/core/rake_task'
require 'rubocop/rake_task'

RuboCop::RakeTask.new

task :default => [:spec, :rubocop]

desc 'Run all specs in spec directory'
RSpec::Core::RakeTask.new(:spec => 'spec:setup') do |t|
  t.pattern = './spec/**/*_spec.rb'
  t.rspec_opts = '--format documentation'
end

namespace :spec do
  desc 'Download required support files for running specs.'
  task :setup do
    def local_mirror(url)
      local_path = 'spec/local_mirror/' + File.basename(url)
      `curl #{url} > #{local_path}` unless File.exist?(local_path)
    end

    FileUtils.mkdir_p 'spec/local_mirror' unless File.directory?('spec/local_mirror')

    local_mirror 'https://s3.amazonaws.com/jruby.org/downloads/9.1.0.0/jruby-complete-9.1.0.0.jar'
    local_mirror 'http://download.eclipse.org/jetty/stable-9/dist/jetty-distribution-9.3.8.v20160314.zip'
    local_mirror 'http://central.maven.org/maven2/org/jruby/rack/jruby-rack/1.1.20/jruby-rack-1.1.20.jar'
  end
end
