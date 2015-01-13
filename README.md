# Datawrapper

Datawrapper is a tool that enables anyone to create visualizations in seconds, without any programming skills.

This fork includes Vagrant setup for local development.

It draws inspiration from [ManyEyes](http://www-958.ibm.com/software/data/cognos/manyeyes/) and [GoogleCharts](https://developers.google.com/chart/) but remains entirely open-source and independent from a third-party server.

It was created by [Mirko Lorenz](http://www.mirkolorenz.com/), [Nicolas Kayser-Bril](http://nkb.fr) and [Gregor Aisch](http://driven-by-data.net/) and was funded by [ABZV](http://www.abzv.de/).

* Live service: <http://datawrapper.de/>
* Documentation: <http://docs.datawrapper.de/> ([Install](https://github.com/datawrapper/datawrapper/wiki/Installing-Datawrapper))

## Getting set up with Vagrant

Run

```
  bootstrap/vagrant.sh
```

Which will ensure that you have the `vagrant-dns` plugin installed.

```
  vagrant dns --install
  vagrant dns --start
```

Which will register a DNS resolver for local development, resolving
`.local` domains.

Then run

```
  vagrant up
```

to boot the virtual machine

## Tidying up

To remove the DNS configuration run:

```
   vagrant dns --uninstall
   vagrant dns --purge
```

## Contact

* IRC: #datawrapper on [freenode.net](https://webchat.freenode.net/)
* Twitter: [@datawrapper](http://twitter.com/datawrapper)
* Blog: [blog.datawrapper.de](http://blog.datawrapper.de)

## Translators

* French - [Anne-Lise Bouyer](https://crowdin.net/profile/annelise)
* Spanish - [Miguel Paz](https://github.com/miguelpaz)
* Italian - [Alessio Cimarelli](https://crowdin.net/profile/jenkin), [nelsonmau](https://crowdin.net/profile/nelsonmau)
* Chinese - [CUI Anyong](https://github.com/xiaoyongzi)
* Portuguese - [Rubens Fernando](https://crowdin.net/profile/rubensfernando)

If you want to contribute translations, contact us via [Crowdin.net](https://crowdin.net/project/datawrapper).
