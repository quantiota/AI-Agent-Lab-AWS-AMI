# AI Agent Lab — AWS AMI

A ready-to-launch **host image** for the [AI Agent Lab](https://github.com/quantiota/AI-Agent-Lab).
It's **Ubuntu 24.04** prepared with everything the lab needs to run, so you skip the host
setup and go straight to launching the stack.

What's baked in (see [`host-setup/`](https://github.com/quantiota/AI-Agent-Lab-AWS-AMI/tree/main/host-setup) for the exact scripts):

- **Docker Engine** + **Compose**
- **Prometheus 3.12** + **node_exporter** (host metrics)
- **rsnapshot** (scheduled backups)
- **recovery-agent** (host-side restore service)
- **git**

> This image is **host preparation only** — it does **not** contain the lab itself or any
> secrets. You clone the lab and configure it after launch (below).

## Public AMI IDs

| Region | AMI ID |
|--------|--------|
| `us-east-2` (Ohio) | `ami-0e1b7cd800de666a8` |
| `eu-central-1` (Frankfurt) | `ami-067e0e4a6afd32b08` |
| `ap-southeast-1` (Singapore) | `ami-0e60b60c848292caf` |
| `ap-northeast-1` (Tokyo) | `ami-06e5983b892ef5568` |



## Launch

1. **EC2 → Launch instance → "My AMIs" / paste the AMI ID** for your region.
2. **Instance type:** at least **8 GB RAM** (e.g. `m7i-flex.large`); 16 GB (`m7i.xlarge`) for comfort.
3. **Root volume:** **≥ 80 GB** gp3 — the lab's container images alone need it.
4. **Security group — open inbound:** `80`, `443`, `22`, `8812` (QuestDB pg-wire), `9009` (QuestDB ILP).
5. Note the instance's **public IP**.

## Then: set up the lab

```bash
ssh -i your-key.pem ubuntu@<public-ip>
git clone https://github.com/quantiota/AI-Agent-Lab.git ~/AI-Agent-Lab
```
Point your domain's subdomains (`vscode`, `questdb`, `grafana`, `aiagentui`, `auth`, `gradio`)
at the public IP, then follow the **AI Agent Lab README** to configure secrets/TLS and bring
the stack up.



## License

MIT 
