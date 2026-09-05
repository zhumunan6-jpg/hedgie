# 🦔 Open Hedgie — User Guide

> Version 2.5.9 · A single-file household finance app. No server, no install, no dependencies.

Full documentation is available on the [GitHub Wiki](https://github.com/lancebramsay/hedgie/wiki).

## Core workflow

1. Use **Log a purchase** for expenses. Expenses remain categorized and can include a vendor, note, date, or recurring bill.
2. Use **Log income** for money received. Income has a source instead of a category and supports one-time, monthly, yearly, or custom recurring schedules.
3. Set a target in **Monthly savings target**. The dashboard calculates `income - spending` for the current calendar month and shows the result against the target.
4. Use **Monthly report** to switch between monthly figures and the retained **Hibernation View** for yearly spending.

The dashboard's **Total savings** uses all historical income and spending. Monthly report figures use the selected month. Data is saved locally as you edit it, so refreshing the page does not remove income, expenses, recurring schedules, targets, or Den data. Existing cloud-sync profiles remain compatible.

Amounts are stored to two decimal places. Income, spending, savings, and target calculations use cents internally, so values such as `0.10 + 0.20` remain exactly `0.30`.

## Quick links

- [Getting Started](https://github.com/lancebramsay/hedgie/wiki/Getting-Started)
- [Cloud Sync](https://github.com/lancebramsay/hedgie/wiki/Cloud-Sync)
- [PWA Install](https://github.com/lancebramsay/hedgie/wiki/PWA-Install)
- [Data Management](https://github.com/lancebramsay/hedgie/wiki/Data-Management)
- [Encryption](https://github.com/lancebramsay/hedgie/wiki/Encryption)
- [Den features](https://github.com/lancebramsay/hedgie/wiki/Den)
- [NFT licensing & Den unlock](https://github.com/lancebramsay/hedgie/wiki/NFT-Licensing)
- [Community app](https://github.com/lancebramsay/hedgie/wiki/Community-App)
- [Native Hedgie](https://github.com/lancebramsay/hedgie/wiki/Native-Hedgie)
- [Roadmap](https://github.com/lancebramsay/hedgie/wiki/Roadmap)
