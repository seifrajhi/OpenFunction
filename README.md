<div align=center><img  width="334" height="117" src=docs/images/logo.png></div>

## 👀 Overview

**OpenFunction** is a cloud-native open source FaaS (Function as a Service) platform aiming to enable users to focus on their business logic without worrying about the underlying runtime environment and infrastructure. Users only need to submit business-related source code in the form of functions.

<div align=center><img src=docs/images/function-lifecycle.svg></div>

OpenFunction features but not limited to the following:

- Convert business-related function source code to runnable application source code.
- Generate a deployable container image from the converted application source code.
- Deploy the generated container image to the underlying runtime environment such as K8s, and automatically scale up and down according to business traffic, and scale to 0 when there is no traffic.
- Provide event management functions for trigger functions.
- Provide additional functions to manage function versions, ingress management etc.

## ☸ CustomResourceDefinitions

<div align=center><img src=docs/images/openfunction-overview.svg></div>

OpenFunction manages resources in the form of CustomResourceDefinitions (CRD) during the lifecycle of a function. You can learn more about it by visiting [Components](docs/concepts/Components.md) or [Concepts](https://openfunction.dev/docs/concepts/).

## ✔️ Compatibility

### Kubernetes compatibility matrix

The following versions are supported and work as we test against these versions in their respective branches. But note that other versions might work!

| OpenFunction                                                 | Kubernetes 1.17 | Kubernetes 1.18 | Kubernetes 1.19 | Kubernetes 1.20+ |
| ------------------------------------------------------------ | --------------- | --------------- | --------------- | ---------------- |
| [`release-0.3`](https://github.com/OpenFunction/OpenFunction/tree/v0.3.0) | &radic;         | &radic;         | &radic;         | &radic;          |
| [`release-0.4`](https://github.com/OpenFunction/OpenFunction/tree/v0.4.0) | &radic;         | &radic;         | &radic;         | &radic;          |
| [`HEAD`](https://github.com/OpenFunction/OpenFunction/tree/main) | &times;         | &times;         | &radic;         | &radic;          |

## 🚀 QuickStart

### Install OpenFunction

Now you can use `ofn`, the CLI of OpenFunction, to install and uninstall OpenFunction and its dependencies. 

Visit [ofn release](https://github.com/OpenFunction/cli/releases) to select the `ofn` cli to deploy to your cluster.

After that you can install OpenFunction with one command:

```
ofn install --all
```

For more information about ofn install, please refer to [ofn install docs](https://github.com/OpenFunction/cli/blob/main/docs/install.md).

### Sample: Run a function.

If you have already installed the OpenFunction platform, refer to [OpenFunction samples](https://github.com/OpenFunction/samples) to find more samples.

Here is an example of a sync function.

> This function will write "Hello, World!" to the HTTP response.

```go
package hello

import (
	"fmt"
	"net/http"
)

func HelloWorld(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello, World!\n")
}
```

And an async function example.

> This function will receive a greeting message and then send it to "another-target".

```go
package bindings

import (
	"encoding/json"
	"log"
  
	ofctx "github.com/OpenFunction/functions-framework-go/openfunction-context"
)

func BindingsOutput(ctx *ofctx.OpenFunctionContext, in []byte) ofctx.RetValue {
	log.Printf("receive greeting: %s", string(in))
	_ := ctx.Send("another-target", in)
	return 200
}
```

You can also use `ofn` to make a quick demo:

>By default the demo environment will be deleted when the demo finishes.
>You can keep the demo kind cluster for further exploration by `ofn demo --auto-prune=false`
>The demo kind cluster can be deleted by `kind delete cluster --name openfunction`

```shell
ofn demo
```

For more information about ofn install, please refer to [ofn demo docs](https://github.com/OpenFunction/cli/blob/main/docs/demo.md).

### Uninstall OpenFunction

Use `ofn` to uninstall OpenFunction and its dependencies:

```shell
ofn uninstall --all
```

For more information about ofn install, please refer to [ofn uninstall docs](https://github.com/OpenFunction/cli/blob/main/docs/uninstall.md).

## 💻 Development

You can get help on developing this project by visiting [Development Guide](docs/development/README.md).

## 🛣️ Roadmap

[Here](docs/roadmap.md) you can find OpenFunction's roadmap.

## 🏘️ Community

### Community Call

Meeting Info: [Zoom](https://us02web.zoom.us/j/89684762679?pwd=U1JNWVdzbElScVFMSEdQQnV0YnR4UT09) 

Meeting Time: Wednesday at 15:30~16:30 Beijing Time (biweekly, starting from June 23rd, 2021) [Meeting Calendar](https://kubesphere.io/contribution/)

[Meeting notes](https://docs.google.com/document/d/1bh5-kVPegjNlIjjq_e37mS3ZhyXWhmmUaysFgeI9_-o/edit?usp=sharing)

### Contact Us

- Slack [#sig-serverless](https://kubesphere.slack.com/archives/C021XAR3CG3)

## 📊 Stats

![Alt](https://repobeats.axiom.co/api/embed/48814fec53572bf75ac4de9d4f447d2c978b26ee.svg "Repobeats analytics image")