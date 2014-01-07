require 'rake'

task :default do
  system("rake -T")
end

# Support for our internal packaging toolchain.  Most people outside of Puppet
# Labs will never actually need to deal with these.
begin
  load File.join(File.dirname(__FILE__), 'ext', 'packaging', 'packaging.rake')
rescue LoadError
end

begin
  @build_defaults ||= YAML.load_file('ext/build_defaults.yaml')
  @packaging_url  = @build_defaults['packaging_url']
  @packaging_repo = @build_defaults['packaging_repo']
rescue
  STDERR.puts "Unable to read the packaging repo info from ext/build_defaults.yaml"
end

namespace :package do
  desc "Bootstrap packaging automation, e.g. clone into packaging repo"
  task :bootstrap do
    if File.exist?("ext/#{@packaging_repo}")
      puts "It looks like you already have ext/#{@packaging_repo}. If you don't like it, blow it away with package:implode."
    else
      cd 'ext' do
        %x{git clone #{@packaging_url}}
      end
    end
  end

  desc "Remove all cloned packaging automation"
  task :implode do
    rm_rf "ext/#{@packaging_repo}"
  end
end
