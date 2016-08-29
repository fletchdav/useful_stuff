# useful_stuff
Memo for my beloved students

## Summary
- [Keyboard's shortcuts (Mac)](#keyboards-shortcuts-mac)
  - [Special characters](#special-characters)
  - [Navigate](#navigate)
  - [Sublime Text](#sublime-text)
  - [Terminal](#terminal)
  - [Chrome](#chrome)
- [Keyboard's shortcuts (LINUX)](#keyboards-shortcuts-linux)
  - [Sublime Text](#sublime-text-1)
  - [Terminal](#terminal-1)
- [Frequently misunderstood error messages](#frequently-misunderstood-error-messages)
  - [NoMethodError: undefined method `some_method' for some_object:SomeType](#nomethoderror-undefined-method-some_method-for-some_objectsometype)
  - [TypeError: SomeType can't be coerced into SomeOtherType](#typeerror-sometype-cant-be-coerced-into-someothertype)
  - [TypeError: no implicit conversion of SomeType into SomeOtherType](#typeerror-no-implicit-conversion-of-sometype-into-someothertype)
  - [ArgumentError: wrong number of arguments (given N, expected M)](#argumenterror-wrong-number-of-arguments-given-n-expected-m)
  - [PG::Error FATAL "myapp_development" does not exist](#pgerror-fatal-myapp_development-does-not-exist)
  - [ActiveRecord::PendingMigrationError Migrations are pending](#activerecordpendingmigrationerror-migrations-are-pending)
  - [PG::ConnectionBad - could not connect to server: No such file or directory](#pgconnectionbad---could-not-connect-to-server-no-such-file-or-directory-is-the-server-running-locally-and-accepting-connections-on-unix-domain-socket-tmpspgsql5432)
  - [NameError: uninitialized constant ClassName](#nameerror-uninitialized-constant-classname)
  - [ResourcesController#action is missing a template for this request format and variant.](#resourcescontrolleraction-is-missing-a-template-for-this-request-format-and-variant)
- [Conflicts solving](#conflicts-solving)
- [Going further](#going-further)

## Keyboard's shortcuts (Mac)
### Special characters
```ruby
{ # alt + (
} # alt + )
[ # alt + shift + (
] # alt + shift + )
| # alt + shift + l
~ # alt + n
\ # alt + /
```

### Navigate
```ruby
from one program to another                # cmd + tab
from one window to another (same program)  # cmd + `
```

### Sublime Text
```ruby
open a file in current project             # cmd + p (or cmd + t)
move a line upwards in file                # ctrl + cmd + ↑
move a line downwards in file              # ctrl + cmd + ↓
(un)comment lines                          # cmd + /
search in file                             # cmd + f
search in project                          # cmd + shift + f
add package                                # cmd + shift + p
add indentation                            # tab
remove indentation                         # shift + tab
move text cursor to next word              # alt + →
move text cursor to previous word          # alt + ←
move text cursor to end of line            # cmd + →
move text cursor to beginning of line      # cmd + ←
close tab                                  # cmd + w
reopen last tab closed                     # cmd + shift + t
navigate to tab on the right               # cmd + alt + →
navigate to tab on the left                # cmd + alt + ←
```

### Terminal
```ruby
open a new tab                             # cmd + t
close tab                                  # cmd + w
clear window (keeping history)             # ctrl + l
clear window (losing history)              # cmd + k
reach beginning of line                    # ctrl + a
reach end of line                          # ctrl + e
erase the whole line                       # ctrl + u
```

### Chrome
```ruby
open developer tools (elements)            # cmd + alt + i
open developer tools (console)             # cmd + alt + j
change docking location                    # cmd + shift + d

navigate to tab on the right               # cmd + alt + →
navigate to tab on the left                # cmd + alt + ←
open a new tab                             # cmd + t
focus on address bar                       # cmd + l
close tab                                  # cmd + w
reopen last tab closed                     # cmd + shift + t
```

## Keyboard's shortcuts (LINUX)

### Sublime Text
```ruby
open a file in current project             # ctrl + p
move a line upwards in file                # ctrl + shift + ↑
move a line downwards in file              # ctrl + shift + ↓
(un)comment lines                          # ctrl + shift + :
search in file                             # ctrl + f
search in project                          # ctrl + shift + f
add package                                # ctrl + shift + p
add indentation                            # tab
remove indentation                         # shift + tab
move text cursor to next word              # alt + →
move text cursor to previous word          # alt + ←
close tab                                  # ctrl + w
reopen last tab closed                     # ctrl + shift + t
```

### Terminal
```ruby
open a new tab                             # ctrl + shift + t
close tab                                  # ctrl + shift + w
clear window                               # ctrl + L (or type "clear" in terminal)
```

## Frequently misunderstood error messages
The first advice I'll throw here is to **read patiently, entirely, twice** the error message when one occurs.
This can get tricky when you read it from a tiny terminal window, so start by opening it wide to have a clear look at its face.

### Ruby

#### ``NoMethodError: undefined method `some_method' for some_object:SomeType``
It means that `some_object` **on which you call** `.some_method` is not of the right type.
You'll get this error if you try to call a `String` instance method on a `Fixnum` for instance.
Its most frequent expression is when `some_object` is nil:
```ruby
recipe.name
# => NoMethodError: undefined method `name' for nil:NilClass
# `recipe` is nil, it shouldn't!
```

#### `TypeError: SomeType can't be coerced into SomeOtherType`
It means that you're trying to mix apples and oranges. 
```ruby
1 + nil
# => TypeError: nil can't be coerced into Fixnum

2 + "2"
# => TypeError: String can't be coerced into Fixnum
```

#### `TypeError: no implicit conversion of SomeType into SomeOtherType`
Its cousin.
```ruby
"2" + 2
# => TypeError: no implicit conversion of Fixnum into String
```

#### `ArgumentError: wrong number of arguments (given N, expected M)`
It means that you're calling a method that takes M parameters with N arguments.
Either your definition of that method is wrong, either you're calling it with the wrong number of arguments.
```ruby
def full_name(first_name, last_name)
  return first_name.capitalize + " " + last_name.capitalize
end

full_name("boris")
# => ArgumentError: wrong number of arguments (given 1, expected 2)
```

### Rails

#### `PG::Error FATAL "myapp_development" does not exist`
Just run `rails db:create`

#### `ActiveRecord::PendingMigrationError Migrations are pending`
Just run `rails db:migrate`.

#### `PG::ConnectionBad - could not connect to server: No such file or directory Is the server running locally and accepting connections on Unix domain socket "/tmp/.s.PGSQL.5432"?`
It means that PG did not exit gracefully last time your computer was shut off.
Run the following in your terminal:
```bash
rm /usr/local/var/postgres/postmaster.pid
```

#### `NameError: uninitialized constant ClassName`
In most cases, you'll get this error message when you're implementing a gem and you forgot to restart your `rails server` after running `bundle install`.

#### `ResourcesController#action is missing a template for this request format and variant.`
After executing the code in a controller's action, Rails conventionnally renders the template named `action.html.erb` in `app/views/resources`.
It thus means you forgot to generate action's associated view, that you misspelled its filename, or that you misplaced it.

## Conflicts solving
When you can't merge a PR due to conflicts in an `unmergeable_branch`, follow this process:

```ruby
# go to your local master branch
git checkout master

# update your master branch locally with github's master
git pull origin master

# go back to unmergeable_branch
git checkout unmergeable_branch

# merger master in unmergeable branch to solve conflicts locally
git merge master

# now you've fetched all conflicts locally, time to solve them
# open sublime and solve conflicts (locate them with cmd + shift + f <<<<<<<)

# commit your code
git add .
git commit -m "conflict solving"
git push origin unmergeable_branch

# open your PR on github to merge it
hub browse

# merge your PR on github

# go back to your terminal and update your local master with merged files
git checkout master
git pull origin master

# create a new branch for next feature
git checkout -b next_feature
```

## Going further

#### [10 common mistakes using Rails](https://www.toptal.com/ruby-on-rails/top-10-mistakes-that-rails-programmers-make)
#### [The Vital Guide to Ruby on Rails Interviewing](https://www.toptal.com/ruby-on-rails#skill_article_content_title)
