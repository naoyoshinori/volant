volant
====

This 'volant' creates a container with immutable lxc. This container can be repeatedly tested.

## Requirement
* bash
* LXD 3.0 LTS

## Usage

```
volant <command> [<args>]
```

### Command

```
volant init <image>
volant delete
volant start
volant stop
volant status
volant run -- command <args>
volant exec -- <args>
volant login
volant commit
volant rollback
volant info
volant list
```

## Example

Create a container.

```
volant init ubuntu:18.04
```

Edit the 'Volantfile.sh' file created when creating the container.

```
#!/bin/sh

init()
{
  sed -i -e 's|http://archive.ubuntu.com|http://jp.archive.ubuntu.com|g' /etc/apt/sources.list
  dhclient
}

upgrade()
{
  apt update
  apt upgrade -y
}

install()
{
  apt install -y build-essential patch ruby-dev zlib1g-dev liblzma-dev # Nokogiri
  apt install -y sqlite3 libsqlite3-dev # SQLite
  apt install -y nodejs # Node.js
  apt autoremove -y

  cat << EOF > ~/.gemrc
gem: --no-document
EOF

  gem install rails -v "5.2.1"
  gem install bundler -v "1.17.1"
}
```

Volant reads the 'Volantfile.sh' file when the 'run' command is executed. The function of 'Volantfile.sh' can be executed in the container.

```
volant run -- init
volant run -- upgrade
volant run -- install
```

Execute the command on the guest's container.

```
volant exec -- bash
```

It is the start and stop of the container.

```
volant start
volant stop
```

The status of the container. Running and stopping.

```
volant status
```

Delete the container.

```
volant delete
```

## Install

```
git clone https://github.com/naoyoshinori/volant.git
cd ./volant
cp volant /usr/local/bin/volant
```

## Licence

[MIT](https://github.com/naoyoshinori/volant/blob/master/LICENSE)

## Author

[naoyoshinori](https://github.com/naoyoshinori)
