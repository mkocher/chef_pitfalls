# chef_pitfalls

!SLIDE

# Recipes for Disaster 

## mkocher@pivotallabs.com

!SLIDE

# What's a Recipe
 
Recipes are just a list of "resources" (commands) that are executed in order.

What they can do:

- Execute a shell command
- Create Directories
- Template a file
- Copy a group of files

!SLIDE
# Who are you?

``` ruby
execute "download rvm" do
   command "curl -Lsf  ... } | tar xvz -C#{RVM_HOME}/src/rvm --strip 1"
 end
```
!SLIDE
# You are who you say you are.
``` ruby
execute "download rvm" do
  command "curl -Lsf  ... } | tar xvz -C#{RVM_HOME}/src/rvm --strip 1"
  user "pivotal"
end
```
!SLIDE
# Non Blocking Strings
``` ruby
execute "link textmate" do
  command "ln -s /Applications/.../mate /bin/mate"
  only_if !File.exists?(/bin/mate)
end
```

!SLIDE
# Non Blocking Strings
Only unless take a shell command as a string, or a ruby block.
``` ruby
execute "link textmate" do
  command "ln -s /Applications/.../mate /bin/mate"
  only_if { !File.exists(/bin/mate) }
end
```

``` ruby
execute "link textmate" do
  command "ln -s /Applications/.../mate /bin/mate"
  only_if "test -e /usr/local/bin/mate"
end
```
!SLIDE
# mkdir -p

``` ruby
directory "/Users/pivotal/workspace/foo/bar/"
  recursive true
end
```
!SLIDE
# mkdir -p
``` ruby
pivotal$ ls -l /Users/pivotal/workspace/
drwxr-xr-x  1 root  root  170 Nov 16 23:23 foo
```
There is hope though, a base_dir directive _should_ be required for a recursive directory

!SLIDE
## Chef isn't hard, it's just a little different.

!NOTES