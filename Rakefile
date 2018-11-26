require 'yaml'
pipeline_files = FileList.new('*.yml').exclude('pipelines.yml')
team = ENV.fetch("CONCOURSE_TEAM")
directory = ENV.fetch('RESOURCE_NAME')
file 'pipelines.yml' => pipeline_files do
  pipelines = pipeline_files.map do |file|
    name = File.basename(file, ".yml")
    {'name' => name, 'team' => team, 'config_file' => File.join(directory, file)}
  end
  config = { "pipelines" => pipelines.to_a }
  File.open('pipelines.yml', 'w') { |f| f.puts YAML.dump(config) }
end

task :default => 'pipelines.yml'
