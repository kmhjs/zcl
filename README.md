# zcl

ZCL is zsh configuration loader.

# What is this

This plugin loads configuration file defined in pre-defined format.
(Written in [#Format](#Format))
Here, the word 'load' means 'read' the configuration file, and 'map' to arguments
list array by following user specified keys order.
After load task, this plugin calls user specified function with generated
arguments list.

# Usage

1. Clone this project. (Or download `zcl` file)
2. Update your `FPATH` with path to zcl file.
3. Call `autoload -Uz zcl` in `.zshrc` etc.

# Format

Here, configuration file format is defined.
Configuration file is shell-style associated array as follows.

```shell
(
  :name              plugin_1
  :url               http://example.com/repo1
  :install_directory /home/owner/path1
)
(
  :name              plugin_2
  :url               http://example.com/repo2
  :install_directory /home/owner/path2
)
(
  :name              plugin_3
  :url               http://example.com/repo3
  :install_directory /home/owner/path3
)
```

Note that, user could not include ( and ) as key or value parenthesis in current
version.

# Example

_config.zsh_

```
(
  :name plugin_1
  :url  http://example.com/repo1
)
(
  :name plugin_2
  :url  http://example.com/repo2
)
(
  :name plugin_3
  :url  http://example.com/repo3
)
```

```shell
function to_json_structure()
{
  echo "{ \"name\": \"${1}\", \"repository url\": \"${2}\" }"
}
```

Then, let's call the function.

```shell
zcl config.zsh to_json_structure :name :url
```

After run this line, user will get following output.

```
{ "name": "plugin_1", "repository url": "http://example.com/repo1" }
{ "name": "plugin_2", "repository url": "http://example.com/repo2" }
{ "name": "plugin_3", "repository url": "http://example.com/repo3" }
```

# License

This project is distributed under MIT License. See `LICENSE` .

# Misc

Currently, this project is under development.
