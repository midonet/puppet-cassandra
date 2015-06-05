# midonet

#### Table of Contents

1. [Overview](#overview)
2. [Module Description](#module-description)
3. [Setup](#setup)
    * [What midonet affects](#what-midonet-affects)
    * [Beginning with midonet](#beginning-with-midonet)
4. [Usage](#usage)
5. [Reference](#reference)
    * [Cassandra Class Reference](#cassandra)
6. [Limitations](#limitations)
7. [Development](#development)

## Overview

Puppet module for install Apache Cassandra. It may be deprecated in favour of
one of the Puppet's Cassandra tagged modules:
https://forge.puppetlabs.com/modules?utf-8=%E2%9C%93&sort=rank&q=cassandra

## Module Description

MidoNet is an Apache licensed production grade network virtualization software
for Infrastructure-as-a-Service (IaaS) clouds. This module provides the puppet
manifests to install Cassandra, one of its No State DataBase (NSDB) components

To know more details about how MidoNet uses cassandra, check out [midonet
reference
architecture](http://docs.midonet.org/docs/latest/reference-architecture/content/cassandra.html)

## Setup

### What midonet affects

* This module affects the respository sources of the target system as well as
  new packages and their configuration files.

### Beginning with puppet-cassandra

(TODO)

## Usage

TODO

## Reference

### Classes

#### Cassandra

MidoNet needs Cassandra cluster to keep track of living connections. This class
installs cassandra the way that MidoNet needs it.

The easiest way to run the class is:

    include midonet::cassandra

And a cassandra single-machine cluster will be installed, binding the
'localhost' address.

Run a single-machine cluster but binding a hostname or another address
would be:

    class {'midonet::cassandra':
        seeds        => ['192.168.2.2'],
        seed_address => '192.168.2.2'
    }

For cluster of nodes, use the same 'seeds' value, but change the
seed_address of each node:

... On node1:

    class {'midonet::cassandra':
        seeds        => ['node_1', 'node_2', 'node_3'],
        seed_address => 'node_1'
    }

... On node2:

    class {'midonet::cassandra':
        seeds        => ['node_1', 'node_2', 'node_3'],
        seed_address => 'node_2'
    }

... On node3:

    class {'midonet::cassandra':
        seeds        => ['node_1', 'node_2', 'node_3'],
        seed_address => 'node_3'
    }

NOTE: node_X can be either hostnames or ip addresses
You can alternatively use the Hiera's yaml style:

    midonet::cassandra::seeds:
        - node_1
        - node_2
        - node_3
    midonet::cassandra::seed_address: 'node_1'

## Development

We happily will accept patches and new ideas to improve this module. Clone
MidoNet's puppet repo in:

    git clone http://github.com/midonet/puppet-cassandra

and send patches via:

    git review

You can see the state of the patch in:

    https://review.gerrithub.io/#/q/status:open+project:midonet/puppet-cassandra

We are using a Gerrit's rebase-based branching policy. So please, submit a
single commit per change. If a commit has been rejected, do the changes you need
to do and squash your changes with the previous patch:

    git commit --amend

We are using kitchen (http://kitchen.ci) for integration testing and puppet-lint
for syntax code convention. To test the module before send a patch, execute:

    $ rake lint
    $ rake test

## Release Notes

* TODO
