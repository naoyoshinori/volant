volant
====

This 'volant' creates a container with immutable lxc. This container can be repeatedly tested.

## Usage

```
volant <command> <arguments...> [options...]
```

### Command

```
volant init
volant delete
volant start
volant stop
volant status
volant run
volant exec -- <arguments...>
volant snapshot
```

## Example

Create a new project.

```
mkdir my_project
cd my_project
touch Volantfile.sh
```

Create a container.

```
volant init
```

Edit the 'Volantfile.sh' file.

```
#!/bin/sh

apt update
apt upgrade -y
```

Execute 'Volantfile.sh' file with 'run' command.

```
volant run
```

Execute the command on the guest's container.

```
volant exec -- bash
```

Save the state of the guest's container.

```
volant snapshot
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
