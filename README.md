# Helmfile Istio

This Helmfile can be used to install Istio by converting the `istiooperator.yaml` file into manifests, by utilizing the `istioctl manifest generate` command, then converting them into a Helm Chart (bedag/raw), to finally install into the cluster.

## Why

IstioCTL does not provide a good way to `diff` between versions. Using IstioCTL to generate manifests is messy, and it is hard to deal with leftovers. This Helmfile is a good option because it allows you to use Helm to install Istio, which is a much more mature tool.

And why not use the official Helm Chart? Because it is not as complete as the IstioCTL and `istiooperator.yaml` file. For example, check the comments from [this PR](https://github.com/istio/istio/pull/38807).

## How to use

I recommend you to use [asdf-vm](https://asdf-vm.com/) to manage your tools versions. You can use the `.tool-versions` file to install the correct versions of the tools.

You'll need `istioctl` (the version depends on you), `helm`, `helmfile` and `kubectl`. Also, you'll need the `slice` kubectl plugin, which you can install with `kubectl krew install slice`. Tested using MacOS and Linux, distros that can use `bash` as the default shell.

1. Clone this repo
2. Copy the `istiooperator.yaml` file to the root of this repo (overwrite the existing one)
3. Run `helmfile diff` to see the changes that will be applied to the cluster - you can also use `helmfile template` to see the generated manifests
4. Run `helmfile apply` to apply the changes to the cluster
