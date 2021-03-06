# Youtrack ruby gem
Youtrack API client.

Youtrack REST API - https://www.jetbrains.com/help/youtrack/standalone/YouTrack-REST-API-Reference.html.




## Installation
Add this line to your application's Gemfile:

```ruby
gem 'youtrack', github: 'maxivak/youtrack'
```

And then execute:
```bash
$ bundle
```

Or install it yourself as:
```bash
$ gem install youtrack
```


* generate token in Youtrack



# Usage


## client

* specify server url and token to init a client

```
client = Youtrack::Client.new 'http://example.com', 'your_youtrack_token'
```

## custom API request
 
* use method
```
client.request(http_method, path, data, extra_headers={})
```

* example - get the projects list
 
```
client = Youtrack::Client.new 'http://example.com', 'your_youtrack_token'

projects = client.request(:get, '/api/admin/projects', {})

puts "#{projects.inspect}"

[{:id=>"0-0", :$type=>"jetbrains.charisma.persistent.Project"}]



# API request with params
projects = client.request(:get, '/api/admin/projects', {fields: "id,name"})

puts "#{projects.inspect}"

[{:name=>"prj1", :id=>"0-0", :$type=>"jetbrains.charisma.persistent.Project"}]


```

* see REST API - https://www.jetbrains.com/help/youtrack/standalone/api-admin-projects.html#get-api-admin-projects


## Get issue

* get_issue(issue_id)

```
client = Youtrack::Client.new 'http://example.com', 'XXXX'

#
issue_data = client.get_issue 'myproject-10' 

```


## Create issue

* `Youtrack::Client.create_issue(data)` - create issue. returns issue id if created or nil if error.


```
client = Youtrack::Client.new 'http://example.com', 'XXXX'

data = {"summary" => "issue title", "description" => "text text text",}
issue_id = client.create_issue data

if issue_id.nil?
  puts "cannot create issue"
end



```

## Update issue


* `Youtrack::Client.update_issue(issue_id, data)` - update issue data. returns true if updated or false if error.




## Add attachment (photo) to issue

* `Youtrack::Client.issue_add_photo(issue_id, name, filename)` - add new attachment to issue. 
* params:
* `filename` - path to file, 
* `name` - name of the image (any string).







