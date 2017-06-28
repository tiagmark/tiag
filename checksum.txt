file.write(resp.body)require 'tempfile'
require 'net/http'
require 'digest/md5'

file = Tempfile.new('temp_file')

begin
  Net::HTTP.start("domain.tld"){|http|
    resp=http.get("02185773dcb5a468df6b.pdf")
    file.write(resp.body)
  }
  hash=Digest::MD5.hexdigest(File.read(file))
  puts hash
ensure
  file.close
  file.unlink
end
