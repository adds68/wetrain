---
resource: true
categories: [BuildStream]
title: "Install BuildStream"
exclude: true
---

# Installing BuildStream 2017

### BuildStream

BuildStream is a new tool being developed to help build projects that have multiple dependencies with multiple build systems.

More information can be found [here](https://gitlab.com/BuildStream/buildstream)

### Installing

There are a few ways to install buildstream, the two main solutions at this current time are by using Docker or from source.

I will discuss installing from source, as i don't want to install a large tool such as Docker to run the buildtool.

I must stress many of the issues faced are mainly due to running a stable Debian release, so hopefully these will be mitigated in the future.

### Firstly

Download the Buildstream project from the Gitlab link above.

### Secondly

Remove any Ostree dependencies currently installed on your sysetem

{% highlight bash %}

 sudo apt remove gir1.2-ostree-1.0 ostree

{% endhighlight %}

### Thirdly

Download the latest OSTree source from [here](https://github.com/ostreedev/ostree)

'CD' into the directory and run:

{% highlight bash %}
	
  sudo apt install gobject-introspection
  sudo apt install libgirepository1.0-dev 

  sudo mkdir /opt/ostree
  sudo chown $USERNAME /opt/ostree

  ./auotgen.sh
  ./configure --prefix=/opt/ostree
  make
  sudo make install

{% endhighlight %}

Now that we have avoided /usr land, we need to add those install paths to our path
and as we have installed object introspection and built ostree with this capability
we must also specify that on our path.

So you must add:

{% highlight bash %}

  PATH=/opt/ostree/bin:$PATH
  export GI_TYPELIB_PATH=/opt/ostree/lib/girepository-1.0/

{% endhighlight %}
### Finally

Navigate back into the Buildstream git directory and run:

{% highlight bash %}
	
  pip3 install --user -e .

{% endhighlight %}

This installs Buildstream via pip into your local user space, so we also need to
add this to our path.

{% highlight bash %}
  
PATH=/.local/bin/:$PATH

{% endhighlight %}

IT SHOULD NOW WORK!!


