## Disclaimer
- This folder contains my notes about installation of ELK stack on Ubuntu Server.
- It can also act as a guideline on how to set it up, but only for the lab purposes, it is absolutely **NOT** suited for production.
- I am sure that it is also absolutely **NOT** the best way to set it up, and in fact, it is already my third attempt to set everything up properly.
- I am working on this whole lab only for educational purposes, to learn something new and figure things out.

## Why am I installing another server with older version of ELK stack?
- Previous installation of ELK stack 9.1.0 ([server-setup-notes](server-setup-notes)) appeared to have a critical bug which is not allowing me to proceed with my homelab goals.
- Here is the [bug report](https://github.com/elastic/beats/issues/45693) of the exact bug that I experienced.
- I decided to install another VM, with the Ubuntu Server this time, and ELK stack version 8.18.0
- Starting with [ubuntu-server-install.md](./ubuntu-server-install.md)
