---
layout: default
---
# Features

* **Easy configuration** with `elixir_buildpack.config` file
* Use **prebuilt Elixir binaries**
* Allows configuring Erlang
* Consolidates protocols
* Hex and rebar support
* Caching of Hex packages, Mix dependencies and downloads

# Supported Versions

* Erlang - Prebuilt packages (17.5, 17.4, etc)
* Elixir - Prebuilt releases (1.0.5, 0.15.1 etc) or prebuilt branches (master, stable, etc)

# Usage

## Push/Deploy a Cloud Foundry application with this buildpack

```
cf push APPNAME -b https://github.com/gogolok/cloudfoundry-buildpack-elixir
```

## Phoenix

Specify **mix phoenix.server** as the *command* to run using the cf cli or the manifest.yml file.

```
---
application:
- name: my-app
  ...
  command: mix phoenix.server

```

```
cf push APPNAME -b https://github.com/gogolok/cloudfoundry-buildpack-elixir -c "mix phoenix.server"
```

# Public Cloud Foundry Providers

## Pivotal Cloud Foundry

Works by default.

## IBM Bluemix

Works with the *cflinuxfs2* stack.

## Anynines

Currently anynines doesn't support the *cflinuxfs2* stack, so this buildpack won't work at the moment.

# Configuration

Create a `elixir_buildpack.config` file in your app's root dir. The file's syntax is bash.

If you don't specify a config option, then the default option from the buildpack's [`elixir_buildpack.config`](https://github.com/gogolok/cloudfoundry-buildpack-elixir/blob/master/elixir_buildpack.config) file will be used.


__Here's a full config file with all available options:__

```
# Erlang version
erlang_version=17.5

# Elixir version
elixir_version=1.0.5

# Always rebuild from scratch on every deploy?
always_rebuild=false
```


## Specifying Elixir version

* Use prebuilt Elixir release

```
elixir_version=1.0.5
```

* Use prebuilt Elixir branch, the *branch* specifier ensures that it will be downloaded every time

```
elixir_version=(branch master)
```

## Specifying Erlang version

* You can specify an Erlang release version like below

```
erlang_version=17.5
```

## Other notes

* Add your own *Procfile* to your application or use the *command* configuration in the manifest file.

* To make use of consolidated protocols they need to be added to the loadpath. Example: `elixir -pa _build/prod/consolidated -S mix run --no-halt`.
