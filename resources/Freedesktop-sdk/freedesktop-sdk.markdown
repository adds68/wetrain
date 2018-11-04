---
resource: true
categories: [Freedesktop-sdk]
title: "Freedesktop-sdk"
exclude: true
---


# Flatpak

Shipping applications on Linux is no easy task, multiple popular distributions,
with widley different configurations and dependencies and app distribution
technologies, an application developers worst nightmare. But fear not, as
Flatpak is here to try and save you from this nightmare. Flatpak is a tool that
has been developed specifically for the Linux application developer, it aims to
greatly simplify the workflow needed to be able to package/test/ship your
application across a wide range of popular Linux distibutions.

The core concept of Flatpak is "runtimes", you can think of them alomst like a
mini distribution in themselves. Flatpak aims to do this by running on your host
machine, install a runtime on this machine, then run an application on top of
that runtime and manage the interface between your host machine and the
applications, providing a layer of security and ensuring the applications has
all of the system utilies and dependencies it needs to just work!

You can have as many runtimes installed on your machine as you want, there are
currently a few available, one recommended by Flatpak, which is the
freedesktop-sdk, the gnome runtime and the kde-runtime, there are also more
specific runtimes dedicated to gaming. But wait, surely installing several
runtimes on my machine is wasteful and bloated? Yes doing this is not as
effiecient as just downloading the application binary itself, however Flatpak
has actually developed additional tools to prevent his becoming a big issue, the
tool is called ostree, it essentially provides file deduplication, by acting as
a git manager for filesystems. Once you install the freedesktop-sdk runtime,
that is it, you never have to install it again for other applications, and if a
runtime has common dependencies between the freedesktop-sdk runtime, then ostree
is smart enough to deduplicate these files for you.

To create/deploy a flatpak application, you simply have to write a manifest
file, stating the runtime you would like your application to use, the specific
commands your applications needs to build and finally the sources for your
application, along with things like app icons etc. An example can be seen below:

{% highlight json %}

{ "app-id": "org.flatpak.qtdemo", "runtime": "org.kde.Platform",
"runtime-version": "5.11", "sdk": "org.kde.Sdk", "command": "flatpak-demo",
"finish-args": [ "--share=ipc", "--socket=x11", "--socket=wayland",
"--filesystem=host", "--device=dri" ], "modules": [ { "name": "flatpak-demo",
"buildsystem": "cmake-ninja", "config-opts":
["-DCMAKE_BUILD_TYPE=RelWithDebInfo"], "sources": [ { "type": "archive", "url":
"https://github.com/flatpak/qt-flatpak-demo/archive/v1.1.3.tar.gz", "sha256":
"60eb65f51d2225b2405a39f92332819f7cefef050e132135008eddf297fa2a56" } ] } ] }


{% endhighlight %}

# Runtimes

So now you understand Flatpak a little more, it will be useful to understand why
runtimes are so important and some of the features that the developers over at
freedesktop-sdk have been working on, in order to make runtimes even better than
before.

As stated earlier runtimes are almost like mini distributions, they maintain a
set of dependencies, often very similar to a distribution, however they do not
ship a kernel, that is left to Flatpak to handle, when you install the runtime
on your host system. However maintaining such a large list of dependencies is
not an easy task, and this is one of the reasons shipping an application on
Linux has always been difficult, distributon maintainers have to ensure that
applications can run on their specific set of dependencies, which can be
different to other distibutions entirely. Which ultimately then makes it
difficult for application developers to to specifiy a single set of dependencies
that their application is known to run on.

Freedesktop-sdk however are trying to make this process much more easier to
maintain, providing many new features to people who are interested in
maintaining/fixing the runtime. Along side this, they are trying to ensure than
other runtimes can easilty extend the freedesktop-sdk runtime to ensure these
new runtimes benefit from the feature it has to offer.

The first big change for the runtime, was that they switched to a new build
system called BuildStream, which makes it easier to model large build pipelines,
with lots of dependencies and version. Utilising this system has allowed the
runtime to be defined in one single format, YAML. This makes it easy for people
to quickly review the dependencies and discover what versions are being shipped,
along with important details like build flags and patches that have been
applied.

BuildStream also offers the ability to cache the entire build pipeline, in an
online central location, this means that if someone wants to modify/update/add a
dependency to the project, they no longer have to build the entire pipeline from
scratch, which can be a significantly long endevour, instead, buildstream is
smart enough to work out that only a single element has been updated and that
only that and it's dependencies should be rebuilt.

Freedesktop-sdk has also introduced a new tool called libabigail, which is tool
used to check the abi of C/C++ software, which means when new updates/changes
are applied to the runtime, the new version of the runtime can be checked before
release to ensure there has been no unexpected changes, which ultimately results
in broken applications, instead the build is failed and detailed information is
provided on what has changed, meaning it can be reviewed before it actually

An important factor for anyone maintaining a runtime is security, with such a
large dependency tree, it is quite common for vulnerabilities to be announced
for multiple dependencies. There is no automated way to currently track these
vulnerabilities apart from updating to the latest release, which is not always
possible, whilst maintaining ABI for appications that depend on the runtime.
Freedesktop has introduced automatic Ci via gitlab, which checks for the latest
release of a package and also checks for outstanding CVE vulnerabilities against
a list of dependencies. Once a new update or CVE is disovered this can be raised
as a merge request aginst the project and maintainers can then act occordingly,
once this is patched, a new release of the runtime is made and every app
currently using freedesktop-sdk, will automatically recieve these updates,
making the application more secure for the end user.

Finally, freedesktop-sdk is also making it easier for other projects to utilise
the runtime, reducing their development time and also allowing them to inherit
the new secuirty/update features. Utilising BuildStream, the freedesktop-sdk
runtime can be used as a "junction", which essentially allows another runtime
utilising BuildStream to import the entire freedesktop-sdk source and utilise
them as they see fit. An example of this is already being used at Gnome, under
the gnome-build-meta project, more information on this can be found
[[here](https://gitlab.gnome.org/GNOME/gnome-build-meta/blob/master/elements/freedesktop-sdk.bsthttps://gitlab.gnome.org/GNOME/gnome-build-meta/blob/master/elements/freedesktop-sdk.bst)
