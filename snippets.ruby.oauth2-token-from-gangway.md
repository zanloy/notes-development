---
id: SUeyV7KVuyOsAdKR4GM5A
title: Oauth2 Token from Gangway
desc: ''
updated: 1641230213382
created: 1641230205855
---
```ruby
# Example: rake 'setup[user,pass]' # note, no quotes
desc 'Load authentication tokens for testing'
task :setup, [:username, :password] do |_, args|
  require 'faraday'
  require 'yaml'

  ## This no longer works for me since I'm using the cert instead of token for
  # k8 auth.
  # config = YAML.safe_load(File.read(File.expand_path('~/.kube/config')))
  # user = config['users'].first
  # token = ['user']['auth-provider']['config']['id-token']
  # File.open('local/k8_token', 'w') { |file| file.puts token }

  oauth_url = URI('https://oauth.prod8.bip.va.gov/')
  response = Faraday.get oauth_url.merge('/oauth2/start?rd=https://kibana.prod8.bip.va.gov/')
  csrf_cookie = "#{response.headers['set-cookie'].split(';', 2).first};'
  dex_url = URI(response.headers['location'])
  response = Faraday.get(dex_url)
  auth = { 'login' => args.username, 'password' => args.password }
  response = Faraday.post(dex_url.merge(response.headers['location']), auth)
  raise "Oauth2 Login Failed. Status Code: #{response.status}" unless response.status == 303

  response = Faraday.get(dex_url.merge(response.headers['location']))
  response = Faraday.get(response.headers['location']) do |req|
    req.headers['cookie'] = csrf_cookie
  end
  oauth_cookie = /(_oauth2_proxy=[^;]*;)/.match(response.headers['set-cookie'])[1]
  File.open('local/_oauth2_proxy', 'w') { |f| f.puts oauth_cookie }
end
```
