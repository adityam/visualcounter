require 'fileutils'
require 'rake/clean'

def make_tds(name, tex_files, doc_files, src_files)
  tex_dir = "#{name}/tex/context/third/#{name}"
  doc_dir = "#{name}/doc/context/third/#{name}"
  src_dir = "#{name}/source/context/third/#{name}"
  sh "mkdir -p #{tex_dir}"
  sh "mkdir -p #{doc_dir}"
  sh "mkdir -p #{src_dir}"
  tex_files.each do |tex|
    FileUtils.cp tex, tex_dir
  end
  doc_files.each do |doc|
    FileUtils.cp doc, doc_dir
  end
  src_files.each do |src|
    FileUtils.cp src, src_dir
  end
end

def make_zip name
  # Ideally, one could have used
  # sh "zip #{name} #{name}" 
  # but that creates a top level directory #{name}.
  # So, we take the following round about alternative.
  sh "cd #{name} && zip -r ../#{name} ./ && cd ../"
end

def make_documentation file
  sh "context --noconsole --purgeall #{file}"
end

VISUALCOUNTER_TEX  = %W[t-visualcounter.mkvi]
VISUALCOUNTER_DOC  = %W[visualcounter.pdf]
VISUALCOUNTER_SRC  = %W[p-documentation.tex visualcounter.tex]

task :clean_visualcounter do
  sh "rm -rf visualcounter"
end

desc "Make TDS for visualcounter module"
task :visualcounter => :clean_visualcounter do
  make_documentation :visualcounter
  make_tds :visualcounter, VISUALCOUNTER_TEX, VISUALCOUNTER_DOC, VISUALCOUNTER_SRC
  make_zip :visualcounter
end

CLEAN.include('*.zip')


