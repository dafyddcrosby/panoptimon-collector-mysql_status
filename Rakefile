require 'bunchr'

Bunchr.build_dir   = '/tmp/build'
Bunchr.install_dir = '/etc/panoptimon'
collectors_dir = "#{Bunchr.install_dir}/collectors"

Bunchr::Software.new do |t|
  t.name = 'collector-mysql_status'

  t.download_commands << "git clone git@github.com:synthesist/panoptimon-collector-mysql_status.git"
  t.work_dir = 'panoptimon-collector-mysql_status'

  t.install_commands << "rm -rf #{collectors_dir}"

  # Configuration JSON
  t.install_commands << "mkdir -p #{collectors_dir}"
  t.install_commands << "cp -f ./mysql_status.json #{collectors_dir}"

  # Collector executable
  t.install_commands << "mkdir -p #{collectors_dir}/mysql_status"
  t.install_commands << "cp -rf ./mysql_status #{collectors_dir}/mysql_status"

  #CLEAN << "#{collectors_dir}/mysql_status.json"
  #CLEAN << "#{collectors_dir}/mysql_status"
end

Bunchr::Packages.new do |t|
  t.name = 'panoptimon-collector-mysql_status'
  t.version = '0.1.0'
  t.iteration = ENV['BUILD_NUMBER'] || '0'

  t.category = 'Monitoring'
  t.license  = 'BSD'
  t.vendor   = 'Sourcefire'
  t.url      = 'https://github.com/synthesist/panoptimon-collector-mysql_status'
  t.description = 'A MySQL collector for Panoptimon'
  t.include_software('collector-mysql_status')

  t.files << Bunchr.install_dir

  # need to enumerate config files for fpm
  #t.config_files << "#{collectors_dir}/mysql_status.json"
end

# default task executed when `rake` is run with no args.
task :default => ['packages:panoptimon-collector-mysql_status']
