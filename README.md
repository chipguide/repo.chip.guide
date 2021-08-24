# chip.guide mirror of the NTC apt repositories

This is a mirror of the NTC apt repositories, mirrored from the [JF Possibilities'](http://chip.jfpossibilities.com/chip/debian/) mirror.

This mirror was created using [apt-mirror](http://apt-mirror.github.io) and contains all of the original unmodified *.deb packages, signed with NTC's original private key.

## Usage

Update your `/etc/apt/sources.list` as below:

### Original

```
deb http://opensource.nextthing.co/chip/debian/repo jessie main
deb http://opensource.nextthing.co/chip/debian/pocketchip jessie main
```

### New value

```
# Mirror of NTC repos
deb https://repo.chip.guide/chip/debian/repo jessie main
deb https://repo.chip.guide/chip/debian/pocketchip jessie main

# Additional updated packages from the chip.guide repos
deb https://repo.chip.guide/chip/debian/chip.guide ./
```

To use the additional packages repo you will need to add our public key:

```
wget -qO - https://repo.chip.guide/chip/debian/chip.guide/KEY.gpg | sudo apt-key add -
```

You will also need o update your `/etc/apt/preferences` to use the new apt mirror:

### Original

```
Package: *
Pin: origin opensource.nextthing.co
Pin-Priority: 1050
```

### New value

```
Package: *
Pin: origin repo.chip.guide
Pin-Priority: 1050
```

## Troubleshooting


### Public key warning

If you have any key warnings about the NTC GPG key when running `apt`, you could try importing the NTC public key:

```
wget -qO - https://repo.chip.guide/NTC.pub | apt-key add -
```

### _"InRelease is expired"_ warning

This can be fixed by adding this line to the end of your `/etc/apt/apt.conf` file:

```
Acquire::Check-Valid-Until "0";
```

