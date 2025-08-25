---
title: Finding Joy In New Technology
author: fritskarl
date: 2025-08-25 17:02:00 +0100
categories: [Linux, DevOps, Virtualization, Development, AI]
tags: [Omarchy, Unraid, VS-Code, Github-Copilot, RTX-5060-Ti-16GB, HP-Z840]
---

**Finding Joy Again in New Technology**

*— From macOS to a hyper‑personalized Linux stack that powers my web apps, SaaS development, and custom hosting.*

---

### 1. Why I'm moving from macOS to Linux

I spent years building code on macOS: Sublime Text, VS Code, Chrome for debugging, many other browsers for QA, iCloud for sync. It worked, but the closed ecosystem made it hard to:

- **Deploy** scalable services quickly.
- **Run** multiple VMs with GPU‑heavy workloads.
- **Customize** every layer of my stack.

So I'm moving to **Omarchy**, an opinionated Hyprland Arch installation designed for developers who want control and speed without the bloat.

*To be real, I'm not fully moving away from macOS. I use an M3 Max 128GB model which is still great for running medium sized AI models for inference, and it's mobile which my workstation isn't. Also, I just use any OS when I see a need for it, I'm not married to one (shout-out to OpenBSD, I love you).*

---

### 2. Omarchy: The One‑Stop Shop for Developers

> **What is Omarchy?**  
> A ready‑to‑run Arch Linux distro that ships with Hyprland, a full dev stack, and an opinionated package set tuned for modern (web) development.

#### Highlights

| Feature                 | Why It Matters                                                                          |
| ----------------------- | --------------------------------------------------------------------------------------- |
| **Hyprland**            | Dynamic tiling, GPU‑accelerated compositing, ideal for managing dozens of applications. |
| **Pre‑installed stack** | Most of what I need to build and ship SaaS apps.                                        |
| **Configurable**        | Declarative config, reproducible builds, instant results.                               |
| **GPU support**         | Full NVIDIA driver stack for my RTX 5060 Ti 16GB cards (see section 4).                 |

---

### 3. VS Code + GitHub Copilot: The New Pair Programming Duo

VS Code on Linux feels like a natural extension of the editor I used on macOS, but with open‑source flexibility:

- Cross‑platform consistency.
- Robust extensions.
- Seamless AI integration.

Copilot turns my comments into working code snippets, letting me prototype API routes or components in seconds. It’s not a replacement for learning, just an extra pair of hands that speeds up the *thought* process.

On larger code bases I mainly use tab completion, sometimes Edit. But for small projects, like a Chrome Extension, I use Agent mode and just *vibe-code* the whole thing.

---

### 4. Unraid on an HP Z840: Gaming + Dev + Hosting Playground

Unraid is the glue that ties my entire setup together:

| Role                       | Setup                                                                                                                                                                      |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Gaming VMs (2×)**        | Each gets a dedicated RTX 5060 Ti 16GB passed through. I can run high‑FPS games without compromising server performance. Most if not all games on max settings on full HD. |
| **Omarchy VM**             | When the game VMs are off, their GPU resources are reclaimed and handed over to an Omarchy virtual machine, my local dev environment for building SaaS apps.               |
| **Other**                  | Inside Unraid I also run some docker apps to help with work, like a reverse proxy, a password vault (Vaultwarden, in progress) and more that come and go.                  |
| **Steam cache (lancache)** | A Docker container that caches Steam downloads locally, reducing bandwidth usage for both VMs.                                                                             |

> **Why Unraid?**  
> Its web UI is a single pane of glass to manage all these services, and its GPU pass-through capabilities lets me share hardware between gaming and development workloads.

I haven’t yet turned the Z840 into a media server; my focus remains on delivering reliable SaaS products. But the same infrastructure can host a Plex or Jellyfin instance with zero additional cost. In fact, the array is already mostly up and running.

Specs for the interested:

| Component                     | Why I like it                                                                                                                                                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Xeon E5-2667 V4 (2x)**      | These are 8 core 16 thread CPUs with a base clock of 3.2GHz, a single core turbo boost of 3.5GHz and a sustained all core boost of 3.4GHz. 32 threads total, great for many VMs and fast enough for 1080p gaming.              |
| **128GB RAM**                 | This gives plenty of headroom for all the VMs and leaves some for Unraid.                                                                                                                                                      |
| **RTX 5060 Ti 16GB (2x)**     | Great budget cards for 1080p gaming and AI inference. The memory bandwidth is 448 GB/s, which is very close to an M3 Max. Two of them deliver 32GB of VRAM, which is very nice for a budget system.                            |
| **HP Z Turbo Drive Quad Pro** | A PCIe card that offers 4 NVME slots, as the Z840 doesn't have that natively. I use 2 slotes for the gaming VMs and the rest for Unraid cache pool (where the other VMs live). The drives are small 256GB, but enough for now. |
| **SAS Drives (4x)**           | The Z840 has a SAS controller, so 4x 4TB (and a spare) were acquired from a sale. They are used but have only a year and half on them.                                                                                         |
All in all the cost of the whole system was around 1500 moneys (usd or euro, close enough). That is a pretty good deal if you ask me, considering the only other solution to get 32GB of VRAM is an RTX 5090. The 5090 costs 2000 at least, without a computer. It is exactly 4x faster though. Meh, I'll survive, and if I need something fast I'll use the cloud for the job.


---

### 5. Building and Locally Hosting SaaS Apps

With this stack, I can:

1. **Develop** locally in an isolated Omarchy VM, optionally with another VM that mirrors production.
2. **Test** Docker containers on the fly; Unraid's Docker spins up everything quite smoothly.
3. **Deploy** to a local private cluster for test or push to a public cloud with minimal friction.
4. **Scale** by adding more VMs (e.g., another VM instance) or spinning up additional containers.

Because all services run on the same hardware, I can monitor CPU/GPU usage easily and tweak resource limits on the fly, no need to spin up expensive cloud instances for load testing.

---

### 6. The Joy Factor

- **Control**: Omarchy lets me shape my OS exactly how I want it.
- **Privacy**: No more weird daemons analyzing every single image, possibly calling back to Cupertino.
- **Productivity**: VS Code + Copilot turns writing code into a creative act.
- **Power**: Unraid on the Z840 shows that older hardware can still do big things, gaming, dev, and dev/test hosting.
- **Community**: Engaging with peers who share the same passion keeps me inspired. I've found X to be a great place now, after being away for 10 years when Twitter started to suck.

If you’re stuck in a closed ecosystem or looking to build scalable web services on a single machine, consider this approach:

1. Pick an *opinionated* distro (Omarchy) for minimal setup overhead.
2. Use VS Code + Copilot for rapid development (or any other combination, they are very much alike with subtle differences).
3. Re-purpose existing hardware with Unraid, GPU pass-through for gaming, Omarchy VM for dev, Docker/k3s for SaaS hosting.
4. Monitor and tweak resource usage to keep everything humming.

---

### 7. Final Thoughts

Technology should *serve* us, not the other way around. When we give ourselves a flexible, open‑source stack, full control over hardware, AI‑augmented coding, and an easy path from local dev to production, we unlock creativity and joy that were once hidden behind corporate walls. Okay, this last sentence is a bit over the top but you get the gist.

Give it a try: set up Omarchy on Arch ([Work on Omarchy ISO on Github](https://github.com/omacom-io/omarchy-iso)), run VS Code with Copilot, spin Unraid on your workstation, and watch as your web apps, SaaS products, and gaming sessions coexist peacefully. The spark of discovery is back, and it’s brighter than ever.

**Happy hacking!**

*PS: yes, I used AI to prepare this post, but I heavily redacted it to reflect my personal opinions. The model I used is openai/gpt-oss-20b, MXFP4 quant, in LM Studio on Omarchy. ~70 tokens per second on a single RTX 5060 Ti 16GB.*