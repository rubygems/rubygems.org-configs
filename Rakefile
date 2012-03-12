
frontends = %w!f1.rubygems.org f2.rubygems.org!

def ssh(server, cmd)
  sh "ssh #{server} '#{cmd}'"
end

task :upload_nginx do
  frontends.each do |f|
    Dir.open "nginx" do |d|
      d.each do |e|
        next if e == "." || e == ".."
        sh "scp nginx/#{e} #{f}:/etc/nginx/conf.d/#{e}"
      end
    end

    ssh f, "sudo /etc/init.d/nginx restart"
  end
end
