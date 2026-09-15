<p align="center">
  <img src="https://raw.githubusercontent.com/Corium-OS/Corium/main/docs/assets/logo.png"
       alt="Corium" width="140" height="140">
</p>

<h1 align="center">Corium</h1>

<p align="center">
  <strong>An immutable Linux distribution that boots into a Kubernetes node.</strong>
</p>

A complete single-node cluster, in full:

```yaml
#cloud-config
corium:
  role: single
```

That is the entire interface for the common case. Every other field has a
default, and every default can be overridden.

**[Read the docs](https://corium-os.github.io/Corium/)** ·
**[Quick start](https://corium-os.github.io/Corium/docs/guides/quickstart/)** ·
**[Source](https://github.com/Corium-OS/Corium)**

---

## Three ideas, chosen together

**The operating system is a container image.** Corium is built with a
`Containerfile`, pushed to a registry, and versioned by digest. You inspect it
with `podman`, scan it with the scanner you already run, promote it between
environments by moving a tag, and roll it back atomically. There is no separate
image-building toolchain to learn, because the one you use for your applications
already works.

**Kubernetes ships with the OS.** [k0s](https://k0sproject.io/) lives in the
read-only `/usr`. Upgrading Kubernetes means booting a new OS image — one
version axis, one upgrade mechanism, one rollback path. A node is a disposable
artefact rebuilt from a digest, not a machine that accumulates state.

**Configuration is cloud-init.** Not a bespoke API, not a new configuration
language: the mechanism every cloud and hypervisor already speaks. Where
cloud-init does not exist — bare metal, PXE, a preconfigured appliance — the
same schema is read from a file, the kernel command line, or a default baked
into the image. Every field is documented in the
[configuration reference](https://corium-os.github.io/Corium/docs/reference/configuration/).

## What it is not

Corium is not a fleet-management control plane; it provisions nodes and stops
there. It does not fork or patch k0s. It does not invent a configuration
language. Those omissions are the point: the project is an opinionated
integration, and its value is in what it declines to do.

## Prior art, honestly

[Talos Linux](https://www.talos.dev/) is the dominant option here and it is
excellent — it is also an API-driven system with no shell and its own
configuration model, which is a real commitment. [Kairos](https://kairos.io/)
covers similar ground, but deliberately builds its own A/B partition scheme on
an arbitrary base distribution rather than using the OSTree/bootc lineage.

Corium's bet is narrower: that for teams already living in OCI registries and
GitOps, an operating system that *is* an image — built, signed, scanned and
promoted like every other image they ship — is worth more than a bespoke
mechanism, however good.

## Status

**Early.** The architecture is settled and every claim above has been exercised
on real hardware: single nodes, unattended ISO installs, and a three-controller
highly available control plane whose virtual IP was verified by hard-stopping
the controller holding it. It is not ready for anything you would miss.

## Where to go

| | |
|---|---|
| [Documentation](https://corium-os.github.io/Corium/) | Quick start, configuration reference, and the decisions behind the project |
| [Corium-OS/Corium](https://github.com/Corium-OS/Corium) | The operating system: `Containerfile`, agent, and deployment scripts |
| [Examples](https://github.com/Corium-OS/Corium/tree/main/docs/examples) | Single node, workers, add-ons, a custom CNI, and a highly available control plane |
| [Architecture decisions](https://corium-os.github.io/Corium/docs/reference/adr-0001-base-image/) | Why fedora-bootc over Fedora CoreOS, and why ext4 over xfs |

---

<sub>Licensed under MIT.</sub>
