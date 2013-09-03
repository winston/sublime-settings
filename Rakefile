TARGET_DIR = File.expand_path("~/Library/Application Support/Sublime Text 2/Packages/User/")
FILES      = ["Preferences.sublime-settings", "Default (OSX).sublime-keymap"]

desc "Symlink Sublime Settings"
task :symlink do
  FILES.each do |file|
    source = File.join(File.expand_path('.'), file)
    target = File.join(TARGET_DIR, file)

    do_symlink(source, target)
  end

  puts "--> Done!"
end

desc "Undo Sublime Settings"
task :undo_symlink do
  FILES.each do |file|
    target = File.join(TARGET_DIR, file)

    undo_symlink(target)
  end
end

def do_symlink(source, target)
  cmd("rm '#{target}'")                       if File.symlink?(target)
  cmd("mv '#{target}' '#{target}.backup'")    if File.exist?(target)
  cmd("ln -s '#{source}' '#{target}'")
end

def undo_symlink(target)
  if(File.symlink?(target))
    cmd("rm '#{target}'")
    cmd("mv '#{target}.backup' '#{target}'")  if(File.exist?("#{target}.backup"))
  end
end

def cmd(cmd)
  puts "Executing :#{cmd}\n\n"
  `#{cmd}`
end
