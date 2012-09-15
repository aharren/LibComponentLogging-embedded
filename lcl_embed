#!/usr/bin/env ruby

# lcl_e -- LibComponentLogging, embedded

require 'FileUtils'

@usage=<<END
usage: lcl_e <project-name> <symbol-prefix> <folder>
END

def print_usage_and_exit(message = '')
  puts "lcl_e: " + message if message != ''
  puts @usage
  exit
end

def process_symbol(text, project_name, symbol_prefix)
  if text.end_with?('.h') or text.end_with?('.m')
    return text.sub('.', "_" + project_name + '.')
  else
    text = text.gsub('lcl_', symbol_prefix + 'lcl' + '_')
    text = text.gsub('LCL_', symbol_prefix + 'LCL' + '_')
    return text
  end
end

def process_file_name(file, project_name, symbol_prefix)
  folder = File.dirname(file)
  name = File.basename(file)

  if file.end_with?('.template.h')
    puts 'D ' + file
    FileUtils.rm(file)
  else
    newname = name.sub(/(lcl|LCL)[a-zA-Z_]*(\.h|\.m|_)/) {|s| process_symbol(s, project_name, symbol_prefix)}
    puts 'R ' + file + ' -> ' + newname
    FileUtils.mv(file, folder + '/' + newname)
  end
end

def process_file_content(file, project_name, symbol_prefix)
  content = File.read(file)

  newcontent = content.gsub(/(lcl|LCL)[a-zA-Z_]*(\.h|\.m|_)/) {|s| process_symbol(s, project_name, symbol_prefix)}
  newcontent = newcontent.gsub(' -- LibComponentLogging', ' -- LibComponentLogging, embedded, ' + project_name + '/' + symbol_prefix)
  return if content == newcontent

  puts 'M ' + file
  File.open(file, "w") {|f| f.puts newcontent}
end

def main(args)
  project_name = args[0]
  print_usage_and_exit('missing argument <project-name>') if !project_name

  symbol_prefix = args[1]
  print_usage_and_exit('missing argument <symbol-prefix>') if !symbol_prefix

  folder = args[2]
  print_usage_and_exit('missing argument <folder>') if !folder

  Dir.chdir(folder) do
    Dir.glob('**/{lcl,LCL}*{.h,.m}').each do|file|
      process_file_name(file, project_name, symbol_prefix)
    end
    Dir.glob('**/*{.h,.m,.pbxproj}').each do|file|
      if File.file?(file) and !File.dirname(file).start_with?('Build')
        process_file_content(file, project_name, symbol_prefix) if File.file? file
      end
    end
  end
  exit
end

main(ARGV)

