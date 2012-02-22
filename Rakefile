desc "Generate .sass files"
task :generate_sass do
  backup_fix = RUBY_PLATFORM =~ /darwin/ ? "''" : nil

  success = system %Q{
    cd vendor/assets/stylesheets && sass-convert --from scss --to sass --recursive . &&
    mv bootstrap/*.sass bootstrap-sass/ &&
    mv _bootstrap.sass _bootstrap-sass.sass &&
    find . -name '*.sass' -print0 | xargs -0 sed -i #{backup_fix} 's/bootstrap\\//bootstrap-sass\\//g'
  }
  puts $? unless success
end
