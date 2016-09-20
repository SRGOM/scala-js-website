---
layout: tutorial
title: QuickStart tutorial
---

This is how you get started in 5 minutes

## <a name="prerequisites"></a> 

### Sbt

No prior knowledge about tool required. 

On Windows, open PowerShell and type in:

```
$OutPath=$Env:UserProfile+"\"+"Downloads\Sbt.msi"
Invoke-WebRequest 'https://dl.bintray.com/sbt/native-packages/sbt/0.13.12/sbt-0.13.12.msi' -OutFile $OutPath
Start-Process $OutPath
```

On Unix, open the shell of your choice and:

```
wget https://dl.bintray.com/sbt/native-packages/sbt/0.13.12/sbt-0.13.12.tgz
tar xvf sbt-0.13.12.tgz -C $HOME
export PATH=$PATH:$HOME/sbt/bin 
```

Or Manually download from the [Website ](http://www.scala-sbt.org/0.13/tutorial/Setup.html) (>= 0.13.7). 

## Hello world

Create a directory ScalaJSHelloWorld and create the following files with the accompanying content in the editor of your choice inside the directory:

`build.sbt`

{% highlight scala %}
enablePlugins(ScalaJSPlugin)

name := "scalajs-hello-world"

scalaVersion := "2.11.7" // or any other Scala version >= 2.10.2
{% endhighlight %}


`project/plugins.sbt`

{% highlight scala %}
addSbtPlugin("org.scala-js" % "sbt-scalajs" % "{{ site.versions.scalaJS }}")
{% endhighlight %}


`project/build.properties`

{% highlight scala %}
sbt.version=0.13.9
{% endhighlight %}

`src/main/scala/HelloWorld.scala`

{% highlight scala %}
import scala.scalajs.js.JSApp
import scalajs.js.Dynamic.{global => window}


object HelloWorld extends JSApp {
  def main(): Unit = {
    window.document.getElementByTagName( "body" ).textContent = "Hello World!" 
  }
}
{% endhighlight %}

`HelloWorld.html`

{% highlight html %}
<html>
  <body>
    <script type="text/javascript" src="./target/scala-2.11/scalajs-hello-world-fastopt.js"></script>
    <script type="text/javascript">
      HelloWorld().main();
    </script>
  </body>
</html>
{% endhighlight %}

Phew! That was it. You only ever have to change HelloWorld.scala from now on, or make one-liner changes in build.sbt. 

Run: `sbt fastOptJS` from the command line inside ScalaJSHelloWorld directory. You should see an output like this. 

```
    [info] Fast optimizing (...)/scalajs-hello-world/target/scala-2.11/scalajs-hello-world-fastopt.js
    [success] (...)
```

You're good to go, open the html file in your browser. If something is off, start by verifying that the path of generated file in the output above is same as the one you included in `HelloWorld.html`. Or grab us on the [Gitter channel](https://gitter.im/scala-js/scala-js)

That's it. This is a 5 minute quickstart to a world of safe JavaScript with no-further boilerplate. Feel free to add more HTML to your html file and manipulate dom using window. To dissect the steps given here, see the [basic tutorial](../basic/index.html) or refer to our [documentation page](../../doc/index.html) for deeper insights into various aspects of Scala.js.
