# puppet

## install
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install puppet puppet-master
```

## settings
/etc/puppet/manifests/site.pp  
```
# group add
group { "ogalush":
gid => 1001,
ensure => present
}

group { "tendo":
gid => 1002,
ensure => present
}

# user add
user { "ogalush":
ensure => present,
home => "/home/ogalush",
managehome => true,
uid => 1001,
gid => 1001,
shell => "/bin/bash",
comment => "Takehiko Ogasawara",
password => '$6$testtest$5txpZMim8XzgmQ8V0DPQvomReE6CJRHfSQ1gSkhAlsWTqRGY.MqHAVNkW8dc6LbPAZLsiXxl4Ju59YUvCrBen1'
}

user { "tendo":
ensure => present,
home => "/home/tendo",
managehome => true,
uid => 1002,
gid => 1002,
shell => "/bin/bash",
comment => "Tadashi Endo",
password => '$6$testtest$ZhkCNjAyGvDSaqAuzScAS5EWblP.MikFo1hoGHPbRmMujFTu6o1LT3MezAnb.BP4TXl11qUaKKkYeWT671lQq0'
}

# ssh directory
file { "/home/ogalush/.ssh":
ensure => directory,
owner => "ogalush",
group => "ogalush",
mode => "0700"
}

file { "/home/tendo/.ssh":
ensure => directory,
owner => "tendo",
group => "tendo",
mode => "0700"
}

# authorized_keys
file { "/home/ogalush/.ssh/authorized_keys":
ensure => present,
source => [
    "puppet:///modules/authorized_keys/ogalush_keys"
  ],
owner => "ogalush",
group => "ogalush",
mode => "0600"
}

file { "/home/tendo/.ssh/authorized_keys":
ensure => present,
source => [
    "puppet:///modules/authorized_keys/tendo_keys"
  ],
owner => "tendo",
group => "tendo",
mode => "0600"
}

# sudo
file { "/etc/sudoers.d/ogalush":
mode => "0600",
owner => "root",
group => "root",
content => "ogalush ALL=(ALL) ALL",
}

file { "/etc/sudoers.d/tendo":
mode => "0600",
owner => "root",
group => "root",
content => "tendo ALL=(ALL) ALL",
}
```
