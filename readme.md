ROC - Remote Object Call
========================

[![Build Status](https://travis-ci.org/peterdemin/python-roc.png?branch=master)](https://travis-ci.org/peterdemin/python-roc)

ROC is RPC enhancment allowing to manipulate
remote objects like they are local

Why ROC?
========
ROC development was started to support acceptance testing
of distributed systems with [FitNesse](http://fitnesse.org),
[waferslim](https://github.com/peterdemin/waferslim) and
[vagrant](http://vagrantup.com)
System infrastucture may be described as follows:

* Host machine running FitNesse server and SLIM server;
* Set of guests, that are provisioned by vagrant with ROC servers;

When hosts' fixture is invoked by SLIM server, it can access guests' roc servers.

Usage
=====

To start serving your modules on remote machine with ROC:

    python -m "roc" -m <your-module-path> -p <port>

To connect to your instance from host:

    from roc.client import server_proxy, remote_module
    proxy = server_proxy(host='127.0.0.1', port=1234)
    RModule = remote_module(proxy)

To instantiate object on remote machine:

    remote_instance = RModule.RemoteClass(1, 2, 3)

From now every method called on remote_instance will be executed on remote.

When you finished, call `proxy.shutdown()` to, well, shut down remote ROC server.
