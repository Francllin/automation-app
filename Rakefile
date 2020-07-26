require 'yaml'
require 'rake'
require 'json'
require "uri"
require "pry"
require "net/http"
require 'open3'

desc 'Validar de código ruby'
task :rubocop do
  run_rubocop
end

desc 'Retonar nome de simulador ios'
task :get_list_simulator, %i[version] do |_task, args|
  get_list_simulator(args.version)
end

desc 'Gherkin Linter'
task :gherkin_linter do
  run_gherkin_linter
end

desc 'Run Gherkin Linter e Rubocop'
task :run_linters do
  run_linters
end

desc 'fazer upload na sauce'
task :upload_apk do
  upload_apk
end

def run_linters
  run_rubocop
  run_gherkin_linter
end

def run_gherkin_linter
  puts "\nAnalyzing feature files with Cuke Linter..."
  config = '-c cuke_linter/configs.yml'
  output = '-o cuke_linter/cuke_linter_report.txt'
  result = system "cuke_linter #{config} #{output}"
  puts 'There are problems in the feature files! Please, check the results file.' unless result
  puts 'Cuke Linter Analysis finished!'
end

def run_rubocop
  puts 'Analisando código-fonte com o Rubocop...'
  checklist = '-r rubocop/formatter/checkstyle_formatter'
  config = '-c code_analyzer/configs.yml'
  formatter = '-f RuboCop::Formatter::CheckstyleFormatter'
  output = '-o code_analyzer/checkstyle-result.xml -f html -o code_analyzer/index.html'
  system "rubocop #{checklist} #{config} #{formatter} #{output}"
  puts 'Análise concluída!'
end

# exemplo versoes: 13.0, 13.1, 13.2 e 13.3
def get_list_simulator(version)
  version = "iOS-#{version.tr('.', '-')}"
  array_simulator = []
  stdout = Open3.capture3('xcrun simctl list --json')
  data = JSON.parse(stdout.first)
  version_simulador = data['devices']["com.apple.CoreSimulator.SimRuntime.#{version}"]
  raise "This version #{version} of the simulator does not exist \n #{data['devices']}" if version_simulador.nil?

  version_simulador.each { |simulador| array_simulator.push(simulador['name']) }
  puts array_simulator
end

def upload_apk
  file = File.expand_path('', __dir__)
  user = 'curl -u qa_test123456:6c4d9231-92c3-4115-bdd3-d50fdfea7c7d'
  verbo = '-X POST -H "Content-Type: application/octet-stream" '
  url = 'https://saucelabs.com/rest/v1/storage/qa_test123456/product_registration.apk\?overwrite\=true --data-binary'
  file_apk = "@#{file}/app/version/1_0_0/product_registration.apk"
  system "#{user} #{verbo} #{url} #{file_apk}"
end
