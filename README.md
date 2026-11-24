# Knots Legacy Umbrel Community App Store

An [Umbrel](https://umbrel.com) community app store with one app: **Knots Legacy + DATUM**.

[Knots Legacy](https://github.com/DimiH2025/KnotsLegacy) is a Bitcoin full node based on Bitcoin Knots 29.3, built from the last release before RDTS/BIP-110 support was added, with adjustable local anti-spam relay policy. This app runs it together with the [OCEAN DATUM gateway](https://github.com/OCEAN-xyz/datum_gateway), so a home miner can point a rig at their own Umbrel and mine on block templates built by their own node.

**Status: test release.** The app has not been run on a real Umbrel device yet. Expect small fixes after the first real installs.

## What you need

- An Umbrel device (Umbrel Home, a Raspberry Pi, or a PC running umbrelOS).
- A large SSD. The first sync downloads the whole blockchain, which takes days on a home device.
- Your own Bitcoin payout address.

## Install

1. Open your Umbrel and go to the **App Store**.
2. Open the menu at the top right and choose **Community App Stores**.
3. Paste this repository's link and click **Add**.
4. Open the new store and install **Knots Legacy + DATUM**.
5. Open the app and sign in to the DATUM dashboard. The password is shown on the app page in Umbrel.
6. In the dashboard, set your payout address.
7. Point your miners at `stratum+tcp://<your-umbrel>:23334` with any worker name.

## Good to know

- Mining at home is a lottery: one rig has a very small chance of finding a block. With DATUM pooled mining, payouts come from the pool according to its rules.
- The node keeps a transaction index, which DATUM needs, so it cannot run pruned.
- This app uses the same network ports as Umbrel's own Bitcoin node apps (peer-to-peer 8333). Do not run both at the same time.
- Only two ports are published: stratum `23334` and peer-to-peer `8333`. The node's RPC port stays inside the app.
- The container images are `ghcr.io/dimih2025/knots-legacy-node` and `ghcr.io/dimih2025/knots-legacy-datum`, tagged with the release version.

## Repository layout

```
umbrel-app-store.yml        store id (knotslegacy) and name
knotslegacy-node/
  umbrel-app.yml            app manifest
  docker-compose.yml        node and DATUM services
  data/                     data folders (kept in git with .gitkeep)
```

This repository is a copy of the `packaging/umbrel/` folder of the main project. Changes are made there and copied here for each release.

## Support

Report problems at https://github.com/DimiH2025/KnotsLegacy/issues and include the app logs from Umbrel.
