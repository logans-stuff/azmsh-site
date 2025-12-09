---
title: Connecting to Arizona Meshtastic Network
level: protected
---

# Connecting to the Arizona Meshtastic MedFast Network (Protected Test)

## Why MedFast?

We spent about a year on the default LongFast mesh and ran into some serious issues. So we built something better.

### The LongFast Problems

**Firmware chaos** - Nodes running everything from ancient to beta versions that don't play nice together. Like trying to video call between dial-up and fiber.

**Router madness** - People throwing ROUTER mode on rooftop nodes without understanding the consequences:
   - Messages dying before reaching strategic spots
   - One-way communication 
   - Packets colliding
   - Everything getting congested

Can you imagine? You set up a sweet mountaintop node, but valley routers consume all the hops before messages reach you.

### The Solution

We got 15 people together (the "mesheads"), spent a month testing MedFast, and it worked way better. No more router shenanigans, no more firmware conflicts, just solid coverage.

### What ILT Does

The Infrastructure Leadership Team coordinates strategic router placements. ILT members are folks who already run major infrastructure nodes around the state - they've got the mountaintop installations and know what works.

We're here to help coordinate, not control. If you want to run a router, chat with us first so we can make sure it helps rather than hurts.

**Simple guidelines:**
- Update your firmware to v2.6+
- Use CLIENT or CLIENT_MUTE roles
- Talk to ILT before setting up routers

That's it. Since switching, we haven't had the drama other meshes deal with.

Alright, let's get you set up!

---

## Alright, Let's Talk About MedFast (Channel Slot 18)

### The Quick Version

Our MedFast mesh runs on **channel slot 18**, and we've designed it to give you rock-solid coverage across Arizona. All we ask? Just follow these guidelines to keep things running smooth for everyone.

### Firmware - Don't Skip This Part!

**You need at least v2.6.0 or newer**

Look, I get it - updating firmware can feel like a chore. But here's the deal:
- We've moved past v2.5.x (it's old news now)
- v2.6.x is stable and honestly, it's way better
- Grab the latest from [Meshtastic.org](https://meshtastic.org/downloads)

Trust me, you'll thank yourself later.

---

## Setting Up Your Node (This Is Important!)

### Your Home Node Setup

**Set it to: CLIENT**

So, your home node - that's probably the one sitting in your house or maybe on your roof, right? Set that bad boy to CLIENT mode. Here's what that means:

- It'll send, receive, AND help out by rebroadcasting messages
- It's smart about when to rebroadcast (won't spam the network)
- You're being a good mesh citizen

**How to do it:**
```
Device Role: CLIENT
```

Easy peasy.

### Everything Else You Own

**Set it to: CLIENT_MUTE**

Now, for your handheld, your car node, basically anything that's not your main home station? Set those to CLIENT_MUTE. 

What's the deal with CLIENT_MUTE? Well:
- Your messages still go out and come in just fine
- But here's the key - it **doesn't rebroadcast** other people's stuff
- This prevents your portable node from accidentally making things worse
- Super important in busy areas (looking at you, Phoenix metro)

**Configuration:**
```
Device Role: CLIENT_MUTE
```

**When should you use CLIENT_MUTE?**
- That radio in your pocket? Yep.
- Nodes hanging out near your home CLIENT? Absolutely.
- Your car setup in the city? For sure.
- Basically any secondary device? You got it.

Think of it this way - one node does the heavy lifting (CLIENT), the rest just chill and chat (CLIENT_MUTE). Make sense?

---

## ⚠️ Hold Up - Let's Talk About Router Roles

### These Need a Conversation First

Look, I'm gonna be real with you. These modes need some thought before you use them:

- **ROUTER**
- **REPEATER** 
- **ROUTER_LATE**

**Before you set any of these, chat with the ILT.** DM someone, pop into `#i-need-help`, whatever works. We just want to make sure it's going in a spot that actually helps.

### But Why Though?

Great question! So here's what the Meshtastic folks say:

> "Using ROUTER or REPEATER roles unnecessarily can cause serious network issues: Increased risk of packet collision, reduced message delivery rates, decreased effective network range due to unnecessary hop consumption."

In plain English? **A badly placed router screws things up for EVERYONE.**

Here's what happens:
- Your messages die early before reaching the good spots
- Communication becomes one-way (super annoying)
- Packets can't climb mountains because they're stuck in valleys
- Everything gets congested and we all suffer

Can you imagine setting up a router thinking you're helping, only to find out you're actually making things worse? Yeah, let's avoid that.

### Here's How We Handle This

**If someone sets up a router that's causing issues, we'll reach out to chat about it.** The goal is education, not punishment. We want you to understand *why* certain configs cause problems, and we'll work with you to find a better solution.

Most of the time it's just a quick conversation: "Hey, that spot isn't ideal because X, but if you move it to Y, it'll actually help a ton!" 

We're all learning here. Mesh networking is complex, and we've made plenty of mistakes along the way too.

**In extreme cases** - like if someone's actively causing problems and refusing to work with the community after multiple conversations - yeah, we might need to remove them from the Discord. But that's a last resort for bad actors, not an immediate response to a config mistake. We've only had to do that once or twice in over a year with 400+ members.

---

## Our Infrastructure Nodes

### Where We've Got Coverage

We've got solid infrastructure nodes set up around:
- **Phoenix area** 
- **Tucson area**

These are strategically placed on mountains and high points with good line-of-sight coverage and reliable power.

### Got a Cool Location?

If you've got access to something like this, hit us up through the ILT:
- Mountain peaks
- Communication towers
- Tall buildings with roof access
- Any high spot with clear line-of-sight

---

## Want to Put Up Infrastructure? Let's Chat!

### When to Reach Out

Planning to run ROUTER, REPEATER, or ROUTER_LATE? Just hit us up first. We're coordinators, not gatekeepers.

### What We Need to Know

**About the location:**
- GPS coordinates
- Elevation and photos of the viewshed
- Mounting details (tower, building, pole?)
- Power situation

**About the setup:**
- What nodes you can see from there
- Expected coverage area
- Equipment you're using
- Maintenance plan

### How to Contact Us

- **DM an ILT member** on Discord
- **Post in `#i-need-help`**

We'll chat about whether it's a good spot, coordinate with existing infrastructure, and make sure it'll actually help the mesh. Usually pretty quick.

---

## Getting Your Radio Set Up (Step-by-Step)

### Using the Meshtastic App (The Easy Way)

Alright, open up your Meshtastic app and let's do this:

**Step 1: Set your channel**
1. Hit **Radio Configuration** → **Channels**
2. On your **Primary Channel (Index 0)**, set:
   - **Name:** Type in `MedFast`
   - **Modem Preset:** Change it to `MEDIUM_FAST`
   
**Step 2: Set your frequency**
1. Go to **Radio Configuration** → **LoRa**
2. Find **Channel/Frequency Slot** and set it to `18`
3. Make sure **Region** is set right (that's `US915` if you're in the US)

**Step 3: Pick your role**
1. Head to **Device Configuration**
2. For your home node: pick `CLIENT`
3. For everything else: pick `CLIENT_MUTE`

**Step 4: Save and reboot**

Done! That wasn't so bad, was it?

### Using the CLI (For You Command Line Nerds)

For complete CLI commands and recommended settings, check out our full configuration guide:

**👉 [Recommended Configuration Settings](https://azmsh.net/docs/recommended_configuration_settings.html)**

This includes all the optimized settings for:
- Device configuration
- Position settings
- LoRa settings
- Telemetry modules
- Neighbor info

### Want to Keep an Eye on the Public Mesh Too?

No problem! You can add LongFast as a secondary channel. Just remember - running multiple channels uses more airtime.

---

## Stuck? We Got You!

### Need Help Getting Set Up?

Hey, configuring this stuff can be confusing the first time. Here's how to get help:

**Check the basics first:**
1. Pop into the `#how-to` channel on Discord - there's tons of guides there
2. Still stuck? Post in `#i-need-help` and tell us:
   - What radio you're using
   - What firmware version you're on
   - What you're trying to do
   - Maybe throw in a screenshot if it helps

3. **For the technical stuff** - DM an ILT member, they love this stuff

### "Help! Nothing's Working!"

Okay, let's troubleshoot together:

**"I can't see any nodes"**
- Double-check you're on channel slot 18 (it happens to everyone)
- Make sure your modem preset says MEDIUM_FAST
- Is your region set correctly?
- Check your antenna - is it actually screwed in? (Don't laugh, we've all done it)

**"My messages are disappearing"**
- Are you accidentally in ROUTER mode? Switch to CLIENT or CLIENT_MUTE
- Make sure you're on firmware v2.6.0 or newer
- Sometimes a reboot fixes weird stuff

---

## More Stuff to Check Out

### Arizona Meshtastic Docs
- **[Recommended Configuration Settings](https://azmsh.net/docs/recommended_configuration_settings.html)** - All the CLI commands and optimized settings
- **[How to Connect Guide](https://azmsh.net/docs/connect.html)** - Our community setup guide

### Official Meshtastic Docs
- [Meshtastic Documentation](https://meshtastic.org/docs) - Everything you ever wanted to know
- [Device Setup Guide](https://meshtastic.org/docs/configuration/radio/device/)
- [Choosing the Right Role](https://meshtastic.org/blog/choosing-the-right-device-role/)

### Arizona Community
- **Discord:** Where all the action happens - join us for real-time chat!
- **GitHub:** [github.com/ArizonaMeshtasticCommunity](https://github.com/ArizonaMeshtasticCommunity)
- **Node Map:** [view.azmsh.net](https://view.azmsh.net) - See nodes on the mesh

### Firmware Updates
- [Web Flasher](https://flasher.meshtastic.org) - Update firmware in your browser
- [Release Notes](https://meshtastic.org/docs/about/releases/)
