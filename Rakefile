require "bundler/gem_tasks"
require "rake/testtask"

Rake::TestTask.new(:test) do |t|
  t.libs << "test"
  t.libs << "lib"
  t.test_files = FileList["test/**/*_test.rb"]
end

task default: :test

namespace :docker do
  task :build do
    require_relative "lib/pgslice/version"

    system "docker build --pull --no-cache -t ankane/pgslice:latest -t ankane/pgslice:v#{PgSlice::VERSION} .", exception: true
  end

  task :release do
    require_relative "lib/pgslice/version"

    system "docker buildx build --push --pull --no-cache --platform linux/amd64,linux/arm64 -t ankane/pgslice:latest -t ankane/pgslice:v#{PgSlice::VERSION} .", exception: true
  end
end
