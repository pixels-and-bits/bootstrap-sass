require 'rake/testtask'
Rake::TestTask.new do |t|
  t.libs << "test"
  t.test_files = FileList['test/*_test.rb']
  t.verbose = true
end

desc 'Dumps output to a CSS file for testing'
task :debug do
  require 'sass'
  require './lib/bootstrap-sass/compass_functions'
  require './lib/bootstrap-sass/rails_functions'
  path = './vendor/assets/stylesheets'
  engine = Sass::Engine.for_file("#{path}/_bootstrap.scss", syntax: :scss, load_paths: [path])
  File.open('./debug.css', 'w') { |f| f.write(engine.render) }
end

task default: :test

desc "Generate .sass files"
task :generate_sass do
  backup_fix = RUBY_PLATFORM =~ /darwin/ ? "''" : nil

  success = system %Q{
    cd vendor/assets/stylesheets && sass-convert --from scss --to sass --recursive . &&
    rm bootstrap-sass/* &&
    mv bootstrap/*.sass bootstrap-sass/ &&
    mv _bootstrap.sass _bootstrap-sass.sass &&
    find . -name '*.sass' -print0 | xargs -0 sed -i #{backup_fix} 's/bootstrap\\//bootstrap-sass\\//g'
  }
  puts $? unless success
end
